<template>
  <button
    type="button"
    class="btn"
    :class="{
      'btn-primary': type === 'primary',
      'btn-secondary': type === 'secondary',
      'btn-default': type === 'default',
      'btn-success': type === 'success',
      'btn-danger': type === 'danger',
      'btn-outline': type === 'outline',
      'btn-teal': type === 'teal',
      'btn-xs': size === 'xs',
      'btn-sm': size === 'sm',
      'btn-md': size === 'md',
      'btn-lg': size === 'lg',
      'btn-xl': size === 'xl',
      'btn-fullwidth': fullWidth,
      'btn-disabled': disabled,
    }"
    @click="handleClick"
  >
    <transition name="fade" mode="out-in">
      <fa v-if="loading" icon="spinner" spin class="mr-2" />
      <fa v-else-if="icon" :icon="[iconPack, icon]" class="mr-2" />
    </transition>
    <slot />
  </button>
</template>

<script>
export default {
  components: {},
  props: {
    type: {
      type: String,
      default: 'default',
    },
    size: {
      type: String,
      default: 'md',
    },
    icon: {
      type: String,
      default: '',
    },
    iconPack: {
      type: String,
      default: 'fas',
    },
    disabled: {
      type: Boolean,
      default: false,
    },
    loading: {
      type: Boolean,
      default: false,
    },
    fullWidth: {
      type: Boolean,
      default: false,
    },
  },
  emits: ['click'],

  setup(props, { emit }) {
    function handleClick(evt) {
      if (!props.disabled) {
        emit('click', evt)
      }
    }

    return {
      handleClick,
    }
  },
}
</script>

<style scoped>
.btn {
  @apply inline-flex items-center border border-transparent transition-all;
  transition: 150ms cubic-bezier(0.215, 0.61, 0.355, 1);
}

.btn-disabled {
  @apply cursor-not-allowed;
}

/* Primary Button */
.btn-primary {
  @apply text-black bg-vita-sunrise focus:outline-none focus:ring-2 focus:ring-black;
}

.btn-primary:hover {
  background-color: color-mod(theme('colors.vita-sunrise') lightness(+10%));
}

.btn-primary.btn-disabled {
  @apply focus:ring-0 text-gray-500;
  background-color: color-mod(theme('colors.vita-sunrise') lightness(+30%));
}

/* Secondary Button */
.btn-secondary {
  @apply text-white bg-vita-purple focus:outline-none focus:ring-2 focus:ring-offset-0 focus:ring-black;
}

.btn-secondary:hover {
  background-color: color-mod(theme('colors.vita-purple') lightness(-5%));
}

.btn-secondary.btn-disabled {
  @apply focus:ring-0;
  background-color: color-mod(theme('colors.vita-purple') lightness(+20%));
}

/* Default Button */
.btn-default {
  @apply border border-gray-400 text-black bg-white hover:bg-gray-50 hover:border-black focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-gray-400;
}

.btn-default.btn-disabled {
  @apply border-gray-300 text-gray-400 focus:ring-0;
}

/* Outline Button */
.btn-outline {
  @apply text-vita-purple border border-vita-purple hover:bg-vita-purple bg-white hover:text-white focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-vita-purple;
}

.btn-outline.btn-disabled {
  @apply focus:ring-0 hover:bg-white;
  color: color-mod(theme('colors.vita-purple') lightness(+10%));
  border-color: color-mod(theme('colors.vita-purple') lightness(+20%));
}

/* Teal Button */
.btn-teal {
  @apply text-black bg-vita-teal focus:outline-none focus:ring-2 focus:ring-offset-0 focus:ring-black;
}

.btn-teal:hover {
  background-color: color-mod(theme('colors.vita-teal') lightness(+15%));
}

.btn-teal.btn-disabled {
  @apply focus:ring-0 text-gray-500;
  background-color: color-mod(theme('colors.vita-teal') lightness(+30%));
}

/* Danger Button */
.btn-danger {
  @apply text-white bg-danger focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-danger;
}

.btn-danger:hover {
  background-color: color-mod(theme('colors.danger') lightness(+8%));
}

.btn-danger.btn-disabled {
  @apply bg-red-50 text-red-300 focus:ring-0;
}

/* Success Button */
.btn-success {
  @apply text-white bg-success focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-success;
}

.btn-success:hover {
  background-color: color-mod(theme('colors.success') lightness(+5%));
}

.btn-success.btn-disabled {
  @apply bg-green-100 text-green-300 focus:ring-0;
}

/* Button Sizes */
.btn-xs {
  @apply px-3 py-1 text-sm rounded-full;
}

.btn-sm {
  @apply px-4 py-1.5 text-base font-medium rounded-full;
}

.btn-md {
  @apply px-6 py-2 text-lg font-medium rounded-full;
}

.btn-lg {
  @apply px-6 py-3 text-lg font-medium rounded-full;
}

.btn-xl {
  @apply px-7 py-4 text-xl font-semibold rounded-full;
}

/* Utility */
.btn-fullwidth {
  @apply w-full justify-center;
}
</style>
