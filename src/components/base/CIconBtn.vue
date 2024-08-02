<template>
  <button
    class="font-primary btn d-flex align-items-center justify-content-center position-relative text-light fw-medium c-btn border-0 p-0"
    :class="[
      `btn-${variant} hover-bg-${variant}-subtle hover-text-${variant} btn-${size} rounded-${rounded} `,
      { 'c-size': size }
    ]"
    v-bind="$attrs"
    :disabled="disabled"
  >
    <div class="d-flex align-items-center justify-content-center" v-if="!loading">
      <slot></slot>
    </div>
    <div v-else class="spinner-border spinner-border-sm" role="status"></div>
  </button>
</template>

<script>
export default {
  props: {
    variant: {
      type: String,
      default: 'primary'
    },
    size: {
      type: String,
      default: '32px'
    },
    loading: {
      type: Boolean,
      default: false
    },
    disabled: {
      type: Boolean,
      default: false
    },
    loaderPositionAbsolute: {
      type: Boolean,
      default: false
    },
    blurred: {
      type: Boolean,
      default: false
    },
    width: {
      type: String
    },
    height: {
      type: String,
      default: '52px'
    },
    rounded: {
      type: [String, Number],
      default: 'circle'
    }
  }
}
</script>
<style lang="scss" scoped>
.c-btn {
  min-width: v-bind(size);
  width: v-bind(size);
  min-height: v-bind(size);
  height: v-bind(size);
}
</style>
