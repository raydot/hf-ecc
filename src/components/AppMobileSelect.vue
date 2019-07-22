<template>
    <div>
        <multiselect v-model="value" :options="options"></multiselect>
    </div>
</template>

<script>

    import Multiselect from 'vue-multiselect'
    export default {
        name: 'app-mobile-select',
        components: { Multiselect },
        data() {
            return {
                value: null,
                options: ['AEM', 'ANALYTICS', 'UX', 'INFORMATION ARCHITECTURE', 'VISUAL DESIGN', 'SITECORE', 'CX STRATEGY', 'ADOBE DAM', 'TAXONOMY', 'PHOTOGRAPHY', 'ADOBE ANALYTICS']
            }
        }

    }
</script>

<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>

