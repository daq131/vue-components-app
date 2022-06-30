<template>
    <base-card>
        <base-button @click="setSelectedTab('stored-resources')" 
        :mode="storedResButtonMode">
        Stored resources</base-button>
        <base-button @click="setSelectedTab('add-resource')"
        :mode="addResButtonMode">
        Add resource</base-button>
    </base-card>
    <keep-alive>
    <component :is="selectedTab"></component>
    </keep-alive>
</template>

<script>

import StoredResources from './StoredResources.vue'
import AddResource from './AddResource.vue';
export default {
    components: {
        StoredResources,
        AddResource 
    },
    data() {
        return {
            selectedTab: 'stored-resources',
            storedResources: [
                { id: 'official-guide', title: 'Official Guide', description: 'The official Vue decumentation.', link: 'https://vuejs.org'},
                { id: 'google', title: 'Google', description: 'Learn google...', link: 'https://google.com'}
            ]
        }
    },
    // provide resources to all child components, we need to inject them in storedResources component
    provide() {
        return {
        resources: this.storedResources,
        addResource: this.addResource,
        }
    },
    computed: {
        addResButtonMode() {
           return this.selectedTab === 'add-resource' ? null : 'flat';
        },
        storedResButtonMode() {
            return this.selectedTab === 'stored-resources' ? null : 'flat';
        }
    },
    methods: {
        setSelectedTab(tab) {
            this.selectedTab = tab;
        },
        addResource(title, description, url) {
            const newResource = {
            id: new Date().toISOString(),
            title: title,
            description: description,
            link: url
            };
            this.storedResources.unshift(newResource);
            this.selectedTab = 'stored-resources';
        }
    }
}
</script>