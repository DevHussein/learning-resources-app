<script>

import AddResource from '@/components/learning-resources/AddResource.vue';
import StoredResources from '@/components/learning-resources/StoredResources.vue';

export default {
  name: 'TheResources',
  components: { AddResource, StoredResources },
  data() {
    return {
      selectedTab: 'StoredResources',
      storedResources: [{
        id: 'official-guide',
        title: 'Official Guide',
        description: 'The official Vue.js documentation.',
        link: 'https://vuejs.org/'
      },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn to google...',
          link: 'https://www.google.org/'
        }]
    };
  },
  provide() {
    return { resources: this.storedResources, addResource: this.addResource, removeResource: this.removeResource };
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'StoredResources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'AddResource' ? null : 'flat';

    }
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, description, url) {
      const newResouce = { id: new Date().toISOString(), title: title, description: description, link: url };
      this.storedResources.unshift(newResouce);
      this.selectedTab = 'StoredResources';
    },
    removeResource(resId) {
      // this.storedResources = this.storedResources.filter((res) => res.id === resId);
      const resIndex = this.storedResources.findIndex(res => res.id === resId);
      this.storedResources.splice(resIndex, 1);
      console.log(this.storedResources);
    }
  }
};
</script>

<template>
  <BaseCard>
    <BaseButton v-on:click="setSelectedTab('StoredResources')" v-bind:mode="storedResButtonMode">Stored Resources
    </BaseButton>
    <BaseButton v-on:click="setSelectedTab('AddResource')" v-bind:mode="addResButtonMode">Add Resource</BaseButton>
  </BaseCard>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<style scoped>

</style>