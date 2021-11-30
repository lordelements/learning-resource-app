<template>
   <base-card>
     <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode">Store Resources</base-button>
     <base-button @click="setSelectedTab('add-resource')" :mode="addResButtonMode" >Add Resource</base-button>
   </base-card>
   <keep-alive>
   <component :is="selectedTab"></component>
   </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue'
import AddResource from './AddResource.vue'
export default {
    components: {
        StoredResources,
        AddResource
    },
    data() {
        return {
            selectedTab: 'stored-resources',
            storedResources: [
        {
          id: 'official-guide',
          tittle: 'Official Guide',
          description: 'The official Vue.js documentation.',
          link: 'https://vuejs.org'
        },
        {
          id: 'google',
          tittle: 'Google',
          description: 'Learn to google...',
          link: 'https://google.org'
        },
      ],
        };
    },
     provide() {
         return {
             resources: this.storedResources,
             addResource: this.addResource,
             deleteResources: this.removeResource
         };
     },
     computed: {
        storedResButtonMode() {
            return this.setSelectedTab === 'stored-resources' ? null :'flat';
        },
        addResButtonMode() {
            return this.selectedTab === 'add-resource' ? null : 'flat';
        }
     },
    methods: {
        setSelectedTab(tab) {
            this.selectedTab = tab;
        },
        addResource(tittle, description, url) {
            const newResource = {
                id: new Date().toISOString(),
                tittle: tittle,
                description: description,
                link: url
            };
            this.storedResources.unshift(newResource);
            this.selectedTab = 'stored-resources';
        },
        removeResource(resId) {
            // this.storedResources = this.storedResources.filter(
            //     (res) => res.id !==resId
            //     );
            //     // console.log(this.storedResources.length);

            const resIndex = this.storedResources.findIndex(res => res.id === resId);
            this.storedResources.splice(resIndex, 1);
        },
    },
};
</script>