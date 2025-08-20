<template>
    <div v-if="group.purchased.plan">
    <form-row
      label="Payment Method"
      v-model="group.purchased.plan.paymentMethod" />
    <form-row
      label="Plan ID"
      v-model="group.purchased.plan.planId" />
    <form-row
      label="Customer ID"
      v-model="group.purchased.plan.customerId" />
    <form-row
      label="Creation Date"
      v-model="group.purchased.plan.dateCreated" />
    <form-row
      label="Termination Date"
      v-model="group.purchased.plan.dateTerminated" />
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
