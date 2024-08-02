<template>
  <div
    class="position-relative overflow-hidden d-inline-block"
    :class="[{ 'cursor-pointer': cursorPointer }, `rounded-${rounded}`]"
    :style="`min-width: ${width}; width: ${width}; min-height: ${height}; height: ${height}`"
  >
    <h2
      v-if="!imageLoaded || !src"
      class="placeholder h-100 d-flex"
      :class="[`bg-${loaderVariant}`]"
      style="min-height: inherit"
    ></h2>
    <img
      v-show="imageLoaded"
      @load="imageLoaded = true"
      class="h-100 w-100"
      :class="[`object-fit-${objectFit}`]"
      alt="image"
      :src="src"
    />
  </div>
</template>
<script>
export default {
  name: 'CThumb',
  props: {
    src: {
      type: String,
      default: ''
    },
    width: {
      type: String,
      default: ''
    },
    height: {
      type: String,
      default: ''
    },
    rounded: {
      type: [String, Number],
      default: '1'
    },
    loaderVariant: {
      type: String,
      default: 'dark-subtle'
    },
    objectFit: {
      type: String,
      default: 'cover'
    },
    cursorPointer: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      imageLoaded: false
    }
  }
}
</script>
