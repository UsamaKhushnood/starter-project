<template>
  <div
    class="spinner-border"
    :class="`text-${variant}  spinner-border-${size}`"
    role="status"
  ></div>
</template>
<script>
export default {
  props: {
    variant: {
      type: String,
      default: 'white'
    },
    size: {
      type: String,
      default: 'sm'
    }
  }
}
</script>
