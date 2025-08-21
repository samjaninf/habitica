<template>
  <div v-if="hasPermission(user, 'groupSupport')">
    <h2>{{ group.name }}</h2>
    <router-link
      v-if="isGroupPlan"
      :to="{'name': 'groupPlanDetail', 'params': {'groupId': groupId}}">
      Group Plan Page
    </router-link>
    
    <supportContainer
      :title="$t('groupData')"
        :onSave="updateGroup">
      <groupData
        :group="group"
      />
    </supportContainer>
    <supportContainer
      :title="$t('groupPlanSubscription')">
      <groupPlan
        :group="group"
      />
    </supportContainer>
    <supportContainer
      v-if="group.type === 'party'"
      :title="$t('questDetails')">
      <quest
        :group="group"
      />
      </supportContainer>
    <supportContainer
      :title="$t('members')">
      <members
        :group="group"
      />
    </supportContainer>
  </div>
</template>

<script>
import { userStateMixin } from '../../../../mixins/userState';
import supportContainer from '../../supportContainer.vue';
import groupData from './groupData.vue';
import members from './members.vue';
import groupPlan from './groupPlan.vue';
import quest from './quest.vue';

export default {
  components: {
    supportContainer,
    groupData,
    members,
    groupPlan,
    quest,
  },
  mixins: [userStateMixin],
  data () {
    return {
      groupId: '',
      group: {},
    };
  },
  watch: {
    groupId () {
      this.loadGroup(this.groupId);
    },
  },
  mounted () {
    this.groupId = this.$route.params.groupId;
  },
  computed: {
    isGroupPlan () {
      return this.group
        && this.group.purchased
        && this.group.purchased.plan
        && this.group.purchased.plan.planId;
    },
  },
  methods: {
    clearData () {
      this.group = {};
    },
    async loadGroup (groupId) {
      this.$emit('changeGroupId', groupId);
      this.group = await this.$store.dispatch('admin:getGroup', { groupId });

    },
    async updateGroup () {
      if (this.group && !this.group.id) {
        this.group.id = this.group._id || this.groupId; // Ensure group has an id property
      }
      await this.$store.dispatch('guilds:update', { group: this.group });
      this.group = await this.$store.dispatch('admin:getGroup', { groupId: this.group.id })
      await this.$store.dispatch('snackbars:add', {
        title: '',
        text: `Group updated`,
        type: 'info',
      });
    },
  },
};
</script>
