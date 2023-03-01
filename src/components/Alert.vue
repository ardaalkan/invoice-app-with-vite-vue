<template>
  <div :class="containerClass">
    <div class="shrink-0">
      <font-awesome-icon :icon="faUser" :class="iconClass" />
    </div>
    <div class="flex-1 space-y-2">
      <h2 :class="titleClass">title</h2>
      <div :class="contentClass">content</div>
    </div>
    <div class="shrink-0">
      <div>
        <font-awesome-icon :class="closeButtonClass" :icon="close" />
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed } from "vue";
import {
  faUser,
  faInfo,
  faClose,
  faWarning,
  faUserCheck,
} from "@fortawesome/free-solid-svg-icons";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import { cva } from "class-variance-authority";

const intent = "success";

// const props = defineProps({
//   intent: {
//     type: String,
//     validator(value) {
//       return["info", "success", "danger", "warning"].includes(value)
//     },
//   }
// })

export default {
  components: {
    FontAwesomeIcon,
  },
  setup() {
    const userIcon = ref(faUser);
    const userInfo = ref(faInfo);
    const close = ref(faClose);
    const warning = ref(faWarning);
    const checkIcon = ref(faUserCheck);

    const containerClass = computed(() => {
      return cva("flex p-4 rounded-md space-x-3 m-10", {
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
      return cva("w-5 h-5 rounded-md p-0.5", {
        variants: {
          intent: {
            info: "text-blue-700",
            success: "text-green-600",
            warning: "text-orange-500",
            danger: "text-red-700",
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
            success: "text-green-600",
            warning: "text-orange-100",
            danger: "text-red-900",
          },
        },
      })({
        intent: intent,
      });
    });

    const contentClass = computed(() => {
      return cva("text-sm text-blue-800", {
        variants: {
          intent: {
            info: "text-blue-800",
            success: "text-green-900",
            warning: "text-orange-100",
            danger: "text-red-800",
          },
        },
      })({
        intent: intent,
      });
    });

    const closeButtonClass = computed(() => {
      return cva("p-0.5 rounded-md -m-1", {
        variants: {
          intent: {
            info: "text-blue-900/70 hover:text-blue-900 hover:text-blue-600 cursor-pointer",
            success:
              "text-green-900/70 hover:text-green-900 hover:text-green-600 cursor-pointer",
            warning:
              "text-orange-900/70 hover:text-orange-900 hover:text-orange-600 cursor-pointer",
            danger:
              "text-red-900/70 hover:text-red-900 hover:text-red-600 cursor-pointer",
          },
        },
      })({
        intent: intent,
      });
    });

    // const iconComputed = computed(() => {
    //   const icons = {
    //     success: checkIcon,
    //     warning: warning,
    //     danger: warning,
    //     info: userIcon,
    //   };
    //   return icons[intent];
    // });

    return {
      userIcon,
      checkIcon,
      userInfo,
      close,
      warning,
      containerClass,
      iconClass,
      titleClass,
      contentClass,
      closeButtonClass,
    };
  },
};
</script>
