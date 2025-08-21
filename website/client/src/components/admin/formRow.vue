<template>
  <div class="form-group row">
    <label class="col-sm-3 col-form-label"><slot name="label">{{ label }}:</slot></label>
    <div class="col-sm-9"
      :class="editable ? 'editable' : 'col-form-label'">
      <slot>
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
        >
      </slot>
      <div class="form-text text-muted" v-if="$slots.helpText">
        <slot name="helpText"></slot>
      </div>
      <div class="form-text text-muted mt-1" v-if="$slots.subtitle">
        <slot name="subtitle"></slot>
      </div>
    </div>
  </div>
</template>

<script>
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
      type: [String, Boolean],
    },
    inputType: {
      type: String,
      default: 'text',
    },
    editable: {
      type: Boolean,
      default: true,
    },
    rows: {
      default: 3,
    },
  },
};
</script>
