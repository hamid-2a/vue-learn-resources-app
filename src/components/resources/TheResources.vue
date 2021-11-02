<template>
  <BaseCard>
    <BaseButton
      @click="setSelectedTab('stored-resources')"
      :mode="savedResButtonMode"
      class="nav-btn"
    >
      Saved Resources
    </BaseButton>
    <BaseButton
      @click="setSelectedTab('add-resource')"
      :mode="addResButtonMode"
      class="nav-btn"
    >
      Add Resources
    </BaseButton>
  </BaseCard>

  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
  components: {
    StoredResources,
    AddResource,
  },

  data() {
    return {
      selectedTab: 'stored-resources',
      resources: [
        {
          id: 'official-guide',
          title: 'Official guide',
          description: 'The official vue js documentaion',
          link: 'https://vuejs.org',
        },
        {
          id: 'react',
          title: 'React Tutorial',
          description: 'The official React js documentaion',
          link: 'https://reactjs.org/',
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn in google',
          link: 'https://google.com',
        },
        {
          id: 'w3school',
          title: 'W3 schools',
          description: 'different fields with online editor',
          link: 'https://www.w3schools.com',
        },
        {
          id: 'youtube',
          title: 'Youtube',
          description: 'Learn by videos',
          link: 'https://youtube.com',
        },
      ],
    };
  },

  provide() {
    return {
      //to StoredResources
      resources: this.resources,
      //to AddResource
      addResource: this.addResource,
      //to ResourceItem
      deleteResource: this.deleteResource,
    };
  },

  computed: {
    savedResButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },

    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    },
  },

  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
      console.log(this.selectedTab);
    },

    addResource(title, description, link) {
      this.resources.unshift({
        // create an unique id
        id: new Date().toISOString,
        title,
        description,
        link,
      });

      this.selectedTab = 'stored-resources';
    },

    deleteResource(id) {
      const resIndex = this.resources.findIndex((res) => res.id === id);
      this.resources.splice(resIndex, 1);
    },
  },
};
</script>

<style scoped>
.nav-btn {
  margin-right: 5px;
}
</style>