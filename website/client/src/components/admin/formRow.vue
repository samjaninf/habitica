<template>
  <div class="form-group row">
    <label class="col-sm-3 col-form-label"><slot name="label">{{ label }}:</slot></label>
    <div class="col-sm-9"
      :class="editable ? 'editable' : 'col-form-label'">
      <slot>
        <div class="input-group">
        <strong v-if="!editable">
          {{ value || "---" }}
        </strong>
        <textarea
          v-else-if="inputType === 'textarea'"
          :value="value"
          class="form-control"
          :rows="rows"
          @input="$emit('input', $event.target.value)"
        ></textarea>
        <input
          v-else
          :value="value"
          class="form-control"
          :type="inputType"
          @input="$emit('input', $event.target.value)"
          :min="min"
          :max="max"
          :step="step"
        >
        <div class="input-group-append" v-if="suffix || $slots.suffix">
          <slot name="suffix">
            <strong class="input-group-text">
              {{ suffix }}
            </strong>
          </slot>
        </div>
      </div>
      </slot>
      <div class="form-text text-muted" v-if="helpText || $slots.helpText">
        <slot name="helpText">{{ helpText }}</slot>
      </div>
      <div class="form-text text-muted mt-1" v-if="$slots.subtitle">
        <slot name="subtitle"></slot>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  @import '@/assets/scss/colors.scss';
  .input-group-append {
    width: auto;

    .input-group-text {
      border-bottom-right-radius: 2px;
      border-top-right-radius: 2px;
      font-weight: 600;
      font-size: 0.8rem;
      color: $gray-200;
    }
  }
</style>

<script>
import { max } from 'lodash';
import { min } from 'lodash';

export default {
  model: {
    prop: 'value',
    event: 'input',
  },
  props: {
    label: {
      type: String,
    },
    value: {
      type: [String, Boolean, Number],
    },
    inputType: {
      type: String,
      default: 'text',
    },
    editable: {
      type: Boolean,
      default: true,
    },
    helpText: {
      type: String,
    },
    suffix: {
      type: String,
    },
    rows: {
      default: 3,
    },
    min: {
      type: [Number, String],
      default: 0,
      validator(value) {
        return !isNaN(value) && min([value, 0]) === 0;
      },
    },
    max: {
      type: [Number, String],
      validator(value) {
        return !isNaN(value) && max([value, 100]) === 100;
      },
    },
    step: {
      type: [Number, String],
      default: 1,
      validator(value) {
        return !isNaN(value) && min([value, 1]) === 1;
      },
    },
  },
};
</script>
