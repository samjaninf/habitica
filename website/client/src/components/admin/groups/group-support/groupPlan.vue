<template>
    <div v-if="group.purchased.plan">
    <form-row
      label="Payment Method"
      v-model="group.purchased.plan.paymentMethod"
      :editable="false" />
    <form-row
      label="Plan ID"
      v-model="group.purchased.plan.planId"
      :editable="false" />
    <form-row
      label="Customer ID"
      v-model="group.purchased.plan.customerId"
      :editable="false" />
    <form-row
      label="Creation Date"
      v-model="group.purchased.plan.dateCreated"
      :editable="false" />
    <form-row
      label="Termination Date"
      v-model="group.purchased.plan.dateTerminated"
      :editable="false" />
    </div>
</template>

<script>
import formRow from '@/components/admin/formRow.vue';

export default {
  components: {
    formRow,
  },
  props: {
    group: {
      type: Object,
      required: true,
    },
  },
};
</script>
