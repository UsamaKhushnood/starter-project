<template>
  <div ref="tooltip" class="d-inline c-tooltip" role="button">
    <slot></slot>
  </div>
</template>
<script>
export default {
  name: 'CTooltip',
  props: {
    show: {
      type: Boolean,
      default: false
    },
    title: {
      type: String,
      default: ''
    },
    placement: {
      type: String,
      default: 'top'
    },
    trigger: {
      type: String,
      default: 'hover'
    },
    template: {
      type: String,
      default:
        '<div class="tooltip" role="tooltip"><div class="tooltip-arrow"></div><div class="tooltip-inner px-2 py-1 font-size-10 rounded-pill"></div></div>'
    },
    container: {
      type: String,
      default: 'body'
    },
    delay: {
      type: { Number, Object },
      default: {} // { "show": 500, "hide": 100 }
    },
    customClass: {
      type: String,
      default: ''
    }
  },
  mounted() {
    this.initializeTooltip()
  },
  methods: {
    initializeTooltip() {
      import('bootstrap').then((bootstrap) => {
        new bootstrap.Tooltip(this.$refs.tooltip, {
          placement: this.placement,
          container: this.container,
          title: this.title,
          template: this.template,
          trigger: this.trigger,
          customClass: this.customClass,
          delay: this.delay
        })
      })
    }
  }
}
</script>
