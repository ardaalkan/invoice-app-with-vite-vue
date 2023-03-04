<template>
  <div :class="containerClass" v-if="props.show">
    <div class="shrink-0">
      <font-awesome-icon :icon="userIcon" :class="iconClass" />
    </div>
    <div class="flex-1 space-y-2">
      <h2 :class="titleClass">{{ props.title }}</h2>
      <div :class="contentClass"><slot /></div>
    </div>
    <div v-if="props.onDismiss" class="shrink-0">
      <button :class="closeButtonClass" @click="dismiss()">
        <font-awesome-icon :icon="faClose" :class="iconClass" />
      </button>
    </div>
  </div>
</template>

<script setup>
import {
  faUser,
  faClose,
  // faInfo,
  // faWarning,
  // faUserCheck,
} from "@fortawesome/free-solid-svg-icons";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import { cva } from "class-variance-authority";
import { ref, computed } from "vue";
const intent = "info";
const userIcon = ref(faUser);
// const userInfo = ref(faInfo);
// const close = ref(faClose);
// const warning = ref(faWarning);
// const checkIcon = ref(faUserCheck);
function dismiss() {
  if (props.onDismiss) {
    props.onDismiss();
  }
}
const props = defineProps({
  intent: {
    type: String,
    validator(value) {
      return ["info", "success", "danger", "warning"].includes(value);
    },
    default: "info",
  },
  title: String,
  show: {
    type: Boolean,
    default: true,
  },
  onDismiss: Function,
});
const containerClass = computed(() => {
  return cva("flex fixed bottom-0 right-0 p-4 rounded-md space-x-3 m-10", {
    variants: {
      intent: {
        info: "bg-blue-100",
        success: "bg-green-100",
        warning: "bg-orange-100",
        danger: "bg-red-100",
      },
    },
  })({
    intent: intent,
  });
});
const iconClass = computed(() => {
  return cva("w-6 h-6", {
    variants: {
      intent: {
        info: "text-blue-700",
        success: "text-green-500",
        warning: "text-orange-400",
        danger: "text-red-500",
      },
    },
  })({
    intent: intent,
  });
});
const titleClass = computed(() => {
  return cva("font-medium text-black", {
    variants: {
      intent: {
        info: "text-blue-900",
        success: "text-green-900",
        warning: "text-orange-900",
        danger: "text-red-900",
      },
    },
  })({
    intent: intent,
  });
});
const contentClass = computed(() => {
  return cva("text-sm", {
    variants: {
      intent: {
        info: "text-blue-800",
        success: "text-green-800",
        warning: "text-orange-400",
        danger: "text-red-500",
      },
    },
  })({
    intent: intent,
  });
});
const closeButtonClass = computed(() => {
  return cva("p-0.5 rounded-md flex my-auto -m-1", {
    variants: {
      intent: {
        info: "text-blue-900/70 hover:text-blue-900 hover:bg-blue-200",
        success: "text-green-900/70 hover:text-green-900 hover:bg-green-200",
        warning:
          "text-orange-900/70 hover:text-orange-900 hover:bg-orange-200 active:bg-orange-300",
        danger:
          "text-red-900/70 hover:text-red-900 hover:bg-red-200 active:bg-red-300",
      },
    },
  })({
    intent: intent,
  });
});
</script>
