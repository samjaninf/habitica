<template>
    <div>
        <form-row
            label="Quest Identifier"
            v-model="group.quest.key"
            :editable="false" />
        <form-row
            label="Quest Leader"
            v-model="group.quest.leader"
            :editable="false">
            <template slot="subtitle">
                <router-link
                    :to="{'name': 'adminPanelUser', 'params': {'userIdentifier': group.quest.leader}}">
                    {{ group.quest.leader }}
                </router-link>
            </template>
        </form-row>
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
