<template>
  <section
    class="bg-gray-900 w-1/3 mx-auto mt-10 p-2 px-5 rounded-md shadow-2xl"
  >
    <contact-section :contact="state.contact" />
    {{ state.contact }}
    <div>
      <div class="mt-5">
        <heading title="Items" />
        <invoice-items :items="state.items" :AddInvoiceItem="AddInvoiceItem" />
      </div>
      <!-- Summary -->
      <invoice-summary :items="state.items" />
      <hr class="bg-gradient-to-r h-[1px] border-none from-gray-700 mt-5" />
      <div class="actionbar text-right my-5">
        <button @click="onSubmit" class="purple-button">Submit</button>
      </div>
    </div>
  </section>
</template>
<script setup>
import invoiceItems from "../components/invoiceItems.vue";
import invoiceSummary from "../components/invoiceSummary.vue";
import contactSection from "../components/contactSection.vue";
import { reactive, provide, watch } from "vue";
const props = defineProps({
  saveInvoice: Function,
  activeInvoice: [Object, null],
});
const state = reactive({
  contact: {
    contact_name: null,
    email: null,
    city: null,
    country: null,
    zipcode: null,
  },
  items: [],
});
const AddInvoiceItem = () => {
  state.items.push({
    id: new Date().getTime(),
    name: null,
    qty: null,
    unit_price: 0.0,
    total_price: 0.0,
  });
};
const DeleteInvoiceItem = (invoiceItem) => {
  state.items = state.items.filter((i) => i.id !== invoiceItem.id);
  console.log(invoiceItem);
};

provide("DeleteInvoiceItem", DeleteInvoiceItem);

const onSubmit = () => {
  console.log(state);
  props.saveInvoice({
    ...state,
    created_at: new Date(),
    id: new Date().getTime(),
  });
  state.contact = {
    contact_name: null,
    email: null,
    city: null,
    country: null,
    zipcode: null,
  };
};

watch(
  () => props.activeInvoice,
  (activeInvoice) => {
    if (activeInvoice) {
      state.contact = {
        ...activeInvoice.contact,
      };
      state.items = [...activeInvoice.items];
    }
  }
);
</script>
