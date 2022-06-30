<template>
    <base-card>
        <base-button @click="setSelectedTab('stored-resources')">Stored resources</base-button>
        <base-button @click="setSelectedTab('add-resource')">Add resource</base-button>
    </base-card>
    <component :is="selectedTab">
    </component>
</template>

<script>

import StoredResources from './StoredResources.vue'
import AddResorce from './AddResorce.vue';
export default {
    components: {
        StoredResources,
        AddResorce 
    },
    data() {
        return {
            selectedTab: 'stored-resoorces'
        }
    },
    methods: {
        setSelectedTab(tab) {
            this.selectedTab = tab;
        }
    }
}
</script>