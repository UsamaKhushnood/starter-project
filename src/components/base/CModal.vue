<template>
  <div ref="modal" class="modal fade" :class="[`modal-${size}`]" :id="id" v-bind="$attrs">
    <div class="modal-dialog modal-dialog-centered">
      <div class="modal-content border-0 rounded-4">
        <div class="modal-header border-0 p-6 pb-0">
          <div class="col-1"></div>
          <div class="col-10">
            <slot name="title">
              <h5 class="text-center fw-semibold">{{ title }}</h5>
            </slot>
          </div>
          <div class="col-1">
            <CIconBtn @click="hide" variant="primary" class="bg-transparent text-black ms-auto">
              <i class="bi bi-x-lg"></i>
            </CIconBtn>
          </div>
        </div>
        <div class="modal-body">
          <slot></slot>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import * as bootstrap from 'bootstrap'
export default {
  name: 'CModal',
  props: {
    id: {
      type: String,
      default: null,
      required: true
    },
    title: {
      type: String,
      default: null
    },
    bodyClass: {
      type: String,
      default: null
    },
    size: {
      type: String,
      default: 'md'
    },
    minWidth: {
      type: String,
      default: null
    },
    width: {
      type: String,
      default: null
    }
  },

  computed: {
    modal() {
      return new bootstrap.Modal(this.$refs.modal, {
        keyboard: false
      })
    }
  },
  mounted() {
    this.$refs.modal.addEventListener('hide.bs.modal', () => {
      this.$emit('hide')
    })
  },
  methods: {
    show() {
      this.modal.show()
    },
    hide() {
      this.modal.hide()
    }
  }
}
</script>
<style lang="scss" scoped>
.modal {
  background-color: #00000018;
}

.modal-sm {
  .modal-dialog {
    min-width: 380px;
    width: 380px;
  }
}

.modal-lg {
  .modal-dialog {
    min-width: 760px;
    width: 760px;
    max-width: none;
  }
}

.modal-custom {
  .modal-dialog {
    min-width: v-bind(minWidth);
    width: v-bind(width);
    max-width: none;
  }
}

.modal-dialog {
  height: v-bind(height);
}
.modal-body {
  padding: 24px;
}
.modal-close-btn {
  width: 26px;
  height: 26px;
}
</style>
