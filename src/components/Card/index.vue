<template>
  <div
    v-if="!overlay"
    :class="`card rounded-md bg-white dark:bg-slate-800 
   
    ${className}
    
    `"
  >
    <div class="card-body flex flex-col" :class="bodyClass">
      <header
        v-if="title || subtitle || $slots.customHeader"
        class="flex items-center"
        :class="`
      ${imgTop ? 'order-1' : ''}
      ${
        noborder
          ? ''
          : 'border-b border-slate-100 dark:border-slate-700 pb-5  -mx-6 px-6'
      }
      
      `"
      >
        <div v-if="$slots.customHeader" class="flex-1">
          <slot name="customHeader"></slot>
        </div>
        <template v-else>
          <div class="flex-1">
            <div
              v-if="title"
              class="card-title text-white dark:bg-[#1E293B] border-2 bg-[#0F172A] flex"
              :class="titleClass"
            >
              <span class="flex-auto"> {{ title }}</span>
              
            </div>
            <div v-if="subtitle" class="card-subtitle" :class="subtitleClass">
              {{ subtitle }}
            </div>
          </div>
          <div v-if="$slots.header" class="flex-0">
            <slot name="header"></slot>
          </div>
        </template>
      </header>
      <div
        v-if="img"
        class="image-box"
        :class="`
        ${imgTop ? 'order-0' : ''}
        ${gapNull ? '-mx-6 ' : ''}
        ${gapNull && imgTop ? '-mt-6 ' : ''}
        ${gapNull && imgBottom ? '-mb-6 ' : ''}
        
        ${imgBottom ? 'order-3 mt-6' : ' mb-6'}
        
        
        `"
      >
        <img
          :src="img"
          alt=""
          class="block w-full h-full object-cover"
          :class="imaClass"
        />
      </div>

      <div
        :class="imgTop ? 'order-2' : ''"
        class="card-text h-full"
      >
        <slot></slot>
      </div>
    </div>
  </div>
  <div
    v-if="overlay"
    class="rounded-md overlay bg-no-repeat bg-center bg-cover card"
    :class="className"
    :style="{
      backgroundImage: 'url(' + `${img}` + ')',
    }"
  >
    <div
      class="card-body h-full flex flex-col justify-center"
      :class="bodyClass"
    >
      <header class="mb-5">
        <div
          v-if="title"
          class="card-title text-slate-900 dark:text-white"
          :class="titleClass"
        >
          {{ title }}
        </div>
        <div v-if="subtitle" class="card-subtitle" :class="subtitleClass">
          {{ subtitle }}
        </div>
      </header>
      <div class="card-text h-full">
        <slot></slot>
      </div>
    </div>
  </div>
</template>
<script>
import Icon from "@/components/Icon";
export default {
  name: "Card",
  components: {
    Icon,
  },
  props: {
    className: {
      type: String,
      default: "",
    },
    title: {
      type: String,
      default: "",
    },
    titleClass: {
      type: String,
      default: "",
    },
    subtitle: {
      type: String,
      default: "",
    },
    subtitleClass: {
      type: String,
      default: "",
    },
    img: {
      type: String,
      default: "",
    },
    imaClass: {
      type: String,
      default: "",
    },
    imgTop: {
      type: Boolean,
      default: false,
    },
    imgBottom: {
      type: Boolean,
      default: false,
    },
    gapNull: {
      type: Boolean,
      default: false,
    },
    overlay: {
      type: Boolean,
      default: false,
    },
    noborder: {
      type: Boolean,
      default: false,
    },
    bodyClass: {
      type: String,
      default: "p-6",
    },
    icon: {
      type: String,
      default: "",
    },
    customIcon: {
      type: Array,
    },
    iconClass: {
      type: String,
      default: "",
    },
  },
  data() {
    return {
      ico: this.icon,
    };
  },
};
</script>
<style lang="scss" scoped>
.card-title {
  @apply font-medium  capitalize md:text-xl md:leading-[28px] text-lg leading-[24px];
}
.card-subtitle {
  @apply text-sm leading-5 font-medium text-slate-600 dark:text-slate-300 mt-1;
}
.overlay {
  @apply relative z-[1] after:absolute after:inset-0 after:w-full after:h-full after:bg-slate-900 after:bg-opacity-40 after:rounded-md after:z-[-1];
  .card-title,
  .card-subtitle {
    @apply text-white;
  }
}
</style>
