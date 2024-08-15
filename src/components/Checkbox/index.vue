<template>
  <div :class="checkBoxClass">
    <label
      class="flex items-center"
      :class="disabled ? ' cursor-not-allowed opacity-50' : 'cursor-pointer'"
    >
      <input
        type="checkbox"
        class="hidden"
        :disabled="disabled"
        :name="name"
        :value="value"
        v-model="localValue"
        v-bind="$attrs"
      />

      <span
      class="h-4 w-4 border flex-none border-slate-100 dark:border-slate-800 rounded inline-flex ltr:mr-3 rtl:ml-3 relative transition-all duration-150"
        :class="
          localValue
            ? activeClass + ' ring-2 ring-offset-2 dark:ring-offset-slate-800 '
            : 'bg-slate-100 dark:bg-slate-600 dark:border-slate-600'
        "
      >
        <img
          src="@/assets/icon/ck-white.svg"
          alt=""
          class="h-[10px] w-[10px] block m-auto"
          v-if="localValue"
        />
      </span>
      <span
        class="text-slate-500 dark:text-slate-400 text-sm leading-6"
        v-if="label"
        :class="labelClass"
      >
        {{ label }}
      </span>
    </label>
  </div>
</template>
<script>
import { computed, defineComponent } from "vue";
export default defineComponent({
  name: "Checkbox",
  inheritAttrs: false,
  props: {
    label: {
      type: String,
    },
    checked: {
      type: Boolean,
      default: false,
    },
    checkBoxClass: {
      type: String,
      default: '',
    },
    disabled: {
      type: Boolean,
      default: false,
    },
    name: {
      type: String,
      default: "checkbox",
    },
    activeClass: {
      type: String,
      default:
        " ring-black-500  bg-slate-900 dark:bg-slate-700 dark:ring-slate-700 ",
    },
    value: {
      type: null,
    },
    modelValue: {
      type: null,
    },
    labelClass:{
      type: String
    }
  },
  emits: {
    "update:modelValue": (newValue) => ({
      modelValue: newValue,
    }),
  },

  setup(props, context) {
    const localValue = computed({
      get: () => props.modelValue,
      set: (newValue) => context.emit("update:modelValue", newValue),
    });

    return { localValue };
  },
});
</script>
<style lang=""></style>
