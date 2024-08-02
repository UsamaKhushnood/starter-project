<template>
  <div class="c-input-group" :style="{ width: width }">
    <label
      v-if="label"
      class="font-size-15 mb-3"
      :class="[{ required }]"
      :style="`--color: ${requiredColor}`"
      :for="name"
    >
      <slot name="label">
        {{ label }}
      </slot>
    </label>

    <div @click="focusIn">
      <div
        class="position-relative border inputWrapper overflow-hidden d-flex align-items-center"
        :class="[
          { 'bg-body-secondary': disabled },
          { focused },
          name && v[name].$error ? 'border-danger' : `border-${borderColor}`,
          `rounded-${rounded}`,
          inputWrapperClass
        ]"
      >
        <div class="d-flex align-items-center w-100 gap-3">
          <slot name="prefix"></slot>
          <input
            ref="input"
            v-model="value"
            class="form-control text-black border-0 p-0 bg-transparent fw-light rounded-0"
            :class="[inputClass, { 'text-body-tertiary': disabled }]"
            :placeholder="placeholder"
            :disabled="disabled"
            :type="type"
            @blur="focusOut"
            @focus="focusIn"
            :min="min"
            :step="step"
          />
          <slot name="suffix"></slot>
        </div>
      </div>

      <div v-if="name">
        <div v-for="error of v[name].$errors" :key="error.$uid">
          <div class="font-size-10 text-danger mt-2 ms-2">
            <i class="bi bi-exclamation-circle-fill me-1"></i>
            {{ error.$message }}
          </div>
        </div>
      </div>
    </div>
    <p v-if="helperText" class="font-size-12 mt-2 text-primary" :class="helperTextClass">
      {{ helperText }}
    </p>
  </div>
</template>

<script>
export default {
  name: 'CInput',
  emits: ['update:modelValue'],
  props: {
    modelValue: {},
    v: {
      type: Object
    },
    borderColor: {
      type: String,
      default: 'light-200'
    },
    inputClass: {
      type: String,
      default: null
    },
    inputWrapperClass: {
      type: String,
      default: null
    },
    label: {
      type: String,
      default: null
    },
    placeholder: {
      type: String,
      default: null
    },
    hideLabel: {
      type: Boolean,
      default: false
    },
    required: {
      type: Boolean,
      default: false
    },
    disabled: {
      type: Boolean,
      default: false
    },
    name: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: 'text'
    },
    helperTextClass: {
      type: String,
      default: ''
    },
    helperText: {
      type: String,
      default: ''
    },
    requiredColor: {
      type: String,
      default: 'primary'
    },
    customPadding: {
      type: String,
      default: 'py-4 pe-4 ps-4 '
    },
    width: {
      type: String,
      default: 'auto'
    },
    rounded: {
      type: [Number, String],
      default: 'pill'
    },
    min: {
      type: Number,
      default: null
    },
    step: {
      type: Number,
      default: null
    },
    height: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      focused: false
    }
  },
  computed: {
    value: {
      get() {
        return this.modelValue
      },
      set(value) {
        this.$emit('update:modelValue', value)
      }
    }
  },
  methods: {
    focusIn() {
      this.focused = true
      this.$refs.input.focus()
    },
    focusOut() {
      this.focused = false
      if (this.name) {
        this.v[this.name].$touch()
      }
    }
  }
}
</script>

<style lang="scss" scoped>
label.required::after {
  content: ' *';
  color: var(--color);
  font-size: 18px;
}

.form-control {
  &:focus-within {
    box-shadow: none;
  }

  &:focus-visible {
    outline: 0;
  }
}

.inputWrapper {
  padding: 8px 24px;
  min-height: v-bind(height);
}
</style>
