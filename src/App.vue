<template>
  <app-sidebar
    :invoices="invoiceList"
    :editInvoice="editInvoice"
    :deleteInvoice="deleteInvoice"
  />
  <invoice-content
    :saveInvoice="saveInvoice"
    :activeInvoice="state.activeInvoice"
  />
  <Transition
    leave-active-class="duration-300"
    leave-to-class="opacity-0"
    enter-active-class="duration-100"
    enter-to-class="opacity-100"
  >
    <DeleteComponent
      :show="showAlert"
      :on-dismiss="() => (showAlert = false)"
      :deleteInvoice="deleteInvoice"
    />
  </Transition>
</template>

<script setup>
import { ref, reactive } from "vue";
import appSidebar from "./components/appSidebar.vue";
import invoiceContent from "./components/invoiceContent.vue";
import DeleteComponent from "./components/DeleteComponent.vue";

const state = reactive({ activeInvoice: null });
const showAlert = ref(false);
const invoiceList = ref([
  {
    id: new Date().getTime(),
    contact: {
      contact_name: "demo",
      email: "demo@demo.com",
      city: "Demo",
      country: "Demo",
      zipcode: "075",
    },
    items: [
      {
        id: new Date().getTime(),
        name: "Demo Demo",
        qty: 1,
        unit_price: 10.0,
        total_price: 20.0,
      },
    ],
  },
]);
const saveInvoice = (invoice) => {
  // console.log("invoice", invoice);
  invoiceList.value.push(invoice);
};
const editInvoice = (invoice) => {
  // console.log(invoice);
  state.activeInvoice = invoice;
  state.sectionVisible = invoice;
};

const deleteInvoice = (invoice) => {
  console.log(invoice);
  showAlert.value = true;
  if (showAlert.value) {
    console.log(showAlert.value);
  } else {
    showAlert.value = false;
  }
};
</script>
