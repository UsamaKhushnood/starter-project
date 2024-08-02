<template>
  <button
    class="font-primary btn d-flex align-items-center justify-content-center gap-2 position-relative fw-medium c-btn"
    :class="[
      `btn-${variant} gap-${gap} btn-${size} rounded-${rounded}`,
      { 'btn-blurred': blurred },
      { 'c-size': size }
    ]"
    v-bind="$attrs"
    :disabled="loading || disabled"
    @click="nevigate"
  >
    <slot>
      {{ label }}
    </slot>
    <div
      v-if="loading"
      class="spinner-border spinner-border-sm text-white"
      :class="{ 'position-absolute end-0 me-6': loaderPositionAbsolute }"
      role="status"
    ></div>
  </button>
</template>
<script>
export default {
  name: 'CButton',
  props: {
    variant: {
      type: String,
      default: 'primary'
    },
    label: {
      type: String,
      default: ''
    },
    size: {
      type: String,
      default: 'md'
    },
    gap: {
      type: [Number, String],
      default: 2
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
    to: {
      type: String,
      default: null
    },
    width: {
      type: String
    },
    height: {
      type: String,
      default: ''
    },
    rounded: {
      type: [String, Number],
      default: 'pill'
    }
  },
  methods: {
    nevigate() {
      if (this.to) {
        this.$router.push(this.to)
      }
    }
  }
}
</script>
<style lang="scss" scoped>
.btn-blurred {
  backdrop-filter: blur(2.5px);
}

.c-btn {
  padding-inline: 16px;
  color: #fff;
  width: v-bind(width);
  height: v-bind(height);
}
</style>
