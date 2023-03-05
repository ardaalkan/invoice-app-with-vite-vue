<template>
  <div
    v-if="show"
    class="absolute top-10 left-0 right-0 z-50 flex items-center justify-center"
  >
    <div class="bg-gray-900 flex-col p-4 rounded-md space-x-3">
      <div class="flex-1 space-y-2">
        <h2 class="font-medium text-gray-300 text-center m-2">
          Are you sure you really want to delete?
        </h2>
      </div>
      <div class="flex justify-center">
        <div>
          <button
            @click="deleteInvoice(invoice)"
            class="bg-gray-500 text-blue-900/70 hover:text-blue-900 hover:bg-gray-300 rounded-md m-3 p-2 px-8 text-gray-200"
          >
            Yes
          </button>
        </div>
        <div>
          <button
            @click="dismiss()"
            class="bg-gray-500 text-blue-900/70 hover:text-blue-900 hover:bg-gray-300 rounded-md m-3 p-2 px-8 text-gray-200"
          >
            No
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<!-- custom alert -->
<script setup>
const props = defineProps({
  show: {
    type: Boolean,
    default: true,
  },
  onDismiss: Function,
  deleteInvoice: Function,
});

function dismiss() {
  if (props.onDismiss) {
    props.onDismiss();
  }
}
</script>
