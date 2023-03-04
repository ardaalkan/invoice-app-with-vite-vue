<template>
  <button @click="toggleSection" class="purple-button p-3 mt-14 ml-10">
    Add New Invoice
  </button>
  <section
    class="bg-gray-900 mx-auto mt-10 ml-10 p-5 px-5 rounded-md shadow-2xl m-10 w-full"
    :class="{ 'section-bounce': show }"
  >
    <contact-section :contact="state.contact" />
    <!-- {{ state.contact }} -->
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
  <transition
    leave-active-class="duration-300"
    leave-to-class="opacity-0"
    enter-active-class="duration-100"
    enter-to-class="opacity-100"
  >
    <Alerts
      :onDismiss="() => (showAlert = false)"
      :show="showAlert"
      title="Please fill in the all inputs..."
      ><p>Inputs must be fill</p></Alerts
    >
  </transition>
</template>

<script setup>
import invoiceItems from "../components/invoiceItems.vue";
import invoiceSummary from "../components/invoiceSummary.vue";
import contactSection from "../components/contactSection.vue";
import Alerts from "../components/Alerts.vue";
import { reactive, provide, watch, ref } from "vue";

const showAlert = ref(false);

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

const show = ref(false);

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
  // console.log(invoiceItem);
};

const toggleSection = () => {
  // console.log("toggle section!");
  state.contact = {
    contact_name: null,
    email: null,
    city: null,
    country: null,
    zipcode: null,
  };
  show.value = !show.value;
};

provide("DeleteInvoiceItem", DeleteInvoiceItem);

const onSubmit = () => {
  if (
    !state.contact.contact_name ||
    !state.contact.email ||
    !state.contact.city ||
    !state.contact.country ||
    !state.contact.zipcode
  ) {
    showAlert.value = true;
    return;
  }
  // console.log(state);
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
