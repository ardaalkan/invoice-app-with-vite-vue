<template>
  <app-sidebar :invoices="invoiceList" :editInvoice="editInvoice" />
  <invoice-content
    :saveInvoice="saveInvoice"
    :activeInvoice="state.activeInvoice"
  />
</template>

<script setup>
import { ref, reactive } from "vue";
import appSidebar from "./components/appSidebar.vue";
import invoiceContent from "./components/invoiceContent.vue";
const state = reactive({ activeInvoice: null });
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
</script>
