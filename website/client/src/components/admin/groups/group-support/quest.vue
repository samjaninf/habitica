<template>
    <div>
        <form-row
            label="Quest Identifier"
            v-model="group.quest.key"
            />
        <form-row
            label="Quest Leader"
            v-model="group.quest.leader"
            />
        <form-row
            label="Is Quest Active"
            v-model="group.quest.active"
            input-type="checkbox"
            />
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
