<template>
  <ul>
    <resourceItem
      v-for="res in resources"
      :key="res.id"
      :title="res.title"
      :description="res.description"
      :link="res.link"
      :id="res.id"
    />
  </ul>
</template>

<script>
import ResourceItem from './ResourceItem.vue';

export default {
  components: {
    ResourceItem,
  },

  inject: ["resources"],
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>