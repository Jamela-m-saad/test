<template>
  <div
    class="fromGroup relative"
    :class="`${error ? 'has-error' : ''}  ${horizontal ? 'flex' : ''}  ${
      validate ? 'is-valid' : ''
    } `"
  >
    <!-- was : horizontal ? 'flex-0 mr-6 md:w-[110px] w-[60px] break-words' : '' -->
    <label
      v-if="label"
      :class="`${classLabel} ${
        horizontal ? 'flex-0 me-6 md:w-[110px] w-[60px] break-words' : ''
      }  ltr:inline-block rtl:block input-label cursor-default`"
      :for="name"
    >
      {{ label }}</label
    >
    <div class="relative" :class="horizontal ? 'flex-1' : ''">
      <input
        :type="types"
        :max="max"
        :min="min"
        :step="step"
        :name="name"
        :placeholder="placeholder"
        :class="`${classInput} input-control w-full block focus:outline-none h-[40px] ${
          hasPasswordIcon ? 'pe-10' : ''
        } `"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
        :error="error"
        :id="name"
        :readonly="isReadonly"
        :disabled="disabled"
        :validate="validate"
        :autocomplete="autocomplete"
        v-if="!isMask"
      />
      <!-- <cleave
        :class="`cleave input-control block w-full ${classInput} focus:outline-none h-[40px] `"
        :name="name"
        :placeholder="placeholder"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
        :error="error"
        :id="name"
        :readonly="isReadonly"
        :disabled="disabled"
        :validate="validate"
        :options="options"
        v-if="isMask"
        modelValue="modelValue"
      /> -->

      <div
        class="flex text-xl absolute right-[14px] ltr:right-[14px] rtl:left-[14px] top-1/2 -translate-y-1/2"
      >
        <span
          v-if="hasPasswordIcon"
          @click="toggleType"
          class="cursor-pointer text-secondary-500"
        >
          <Icon icon="heroicons-outline:eye" v-if="types === 'password'" />
          <Icon icon="heroicons-outline:eye-off" v-else />
        </span>

        <!--Slot to insert any components inside the textinput-->
        <slot></slot>

        <span v-if="error" class="text-danger-500">
          <Icon icon="heroicons-outline:information-circle" />
        </span>

        <span v-if="validate" class="text-success-500">
          <Icon icon="bi:check-lg" />
        </span>
      </div>
    </div>

    <span
      v-if="error"
      class="mt-2 ms-2"
      :class="
        msgTooltip
          ? ' inline-block bg-danger-500 text-white text-[10px] px-2 py-1 rounded'
          : ' text-danger-500 inline-block text-sm '
      "
      >{{ error }}</span
    >
    <span
      v-if="validate"
      class="mt-2"
      :class="
        msgTooltip
          ? ' inline-block bg-success-500 text-white text-[10px] px-2 py-1 rounded'
          : ' text-success-500 block text-sm'
      "
    >
      <!-- >was {{ validate }}</span -->
    </span>

    <span
      class="block text-secondary-500 font-light leading-4 text-xs mt-2 ms-2"
      :class="classDescription"
      v-if="description"
      >{{ description }}</span
    >
  </div>
</template>
<script>
import Icon from "@/components/Icon";
// import Cleave from "vue-cleave-component";
export default {
  components: { Icon },
  props: {
    placeholder: {
      type: String,
      default: "",
    },
    label: {
      type: String,
    },
    classLabel: {
      type: String,
      default: " ",
    },
    classInput: {
      type: String,
      default: "classinput",
    },
    autocomplete: {
      type: String,
    },
    type: {
      type: String,
      default: "text",
      //required: true,
    },
    name: {
      type: String,
    },
    modelValue: {
      type: [String, Number],
      default: "",
    },
    error: {
      type: String,
    },
    hasPasswordIcon: {
      type: Boolean,
      default: false,
    },
    isReadonly: {
      type: Boolean,
      default: false,
    },
    disabled: {
      type: Boolean,
      default: false,
    },
    horizontal: {
      type: Boolean,
      default: false,
    },
    validate: {
      type: Boolean,
    },
    msgTooltip: {
      type: Boolean,
      default: false,
    },
    description: {
      type: String,
    },
    classDescription: {
      type: String,
      default: " ",
    },
    min: {
      type: Number,
      default: 0,
    },
    max: {
      type: Number,
      default: 10,
    },
    step: {
      type: Number,
    },
    isMask: {
      type: Boolean,
      default: false,
    },
    options: {
      type: Object,
      default: () => ({
        creditCard: true,
        delimiter: "-",
      }),
    },
  },
  data() {
    return {
      types: this.type,
    };
  },

  methods: {
    toggleType() {
      // toggle the type of the input field
      this.types = this.types === "text" ? "password" : "text";
    },
  },
};
</script>
<style lang="scss"></style>
