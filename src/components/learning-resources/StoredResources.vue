<script>
import LearningResource from '@/components/learning-resources/LearningResource.vue';

export default {
  name: 'StoredResources',
  components: { LearningResource },
  inject: ['resources']
};
</script>

<template>
  <ul>
    <LearningResource
      v-for="resource in resources"
      v-bind:id="resource.id"
      v-bind:key="resource.id"
      v-bind:title="resource.title"
      v-bind:description="resource.description"
      v-bind:link="resource.link" />
  </ul>
</template>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>