<template>
  <button :class="closeButtonClass">
    <font-awesome-icon :icon="backward" />
  </button>
</template>

<script setup>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import { cva } from "class-variance-authority";
import { ref, computed } from "vue";
import { faRotate } from "@fortawesome/free-solid-svg-icons";

const backward = ref(faRotate);

const intent = open;

const props = defineProps({
  intent: {
    type: String,
    validator(value) {
      return ["open", "close"].includes(value);
    },
    default: "open",
  },
  onTurn: { Function },
});

const closeButtonClass = computed(() => {
  return cva("p-3 rounded-md mt-3 outline-none ", {
    variants: {
      intent: {
        open: "bg-blue-600",
        close: "bg-green-400",
      },
    },
  })({
    intent: intent,
  });
});
</script>
