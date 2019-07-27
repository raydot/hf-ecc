<template>
    <div class="categorySelector">
        <div v-if="isMobile">
            <app-category-selector-mobile :options="options" />
        </div>
        <div v-else>
            <app-category-selector-desktop :options="options" v-on:toggleprop="toggleprop" />
        </div>
    </div>
</template>

<script>
    /* 
        This "controller" manages the the two application category selectors,
        one for mobile and one for desktop.  It also passes the filter back to the app.  It was getting too hairy to manage all of these things in one place, especially with the mobile and DTP functionality being different.

        This also means only one place to send the data.
    */
    import { isMobile } from 'mobile-device-detect'
    import AppCategorySelectorDesktop from '@/components/AppCategorySelectorDesktop.vue'
    import AppCategorySelectorMobile from '@/components/AppCategorySelectorMobile.vue'
    
    export default {
        name: 'app',
        props: ['options'],
        components: {
            AppCategorySelectorMobile,
            AppCategorySelectorDesktop,
        },
        data: function() {
            // Options could be populated from REST or similar,
            // or even dynamically derived from the JSON itself.
            return {
                isMobile: isMobile,
                filterList: []
            }
        },
        methods: {
            // Add / remove selected items to the filter
            toggleprop(whichProp) {
                var index = this.filterList.indexOf(whichProp)
                index === -1
                    ? this.filterList.push(whichProp)
                    : this.filterList.splice(index, 1)
                this.$root.$emit('toggleapproot', this.filterList)
            }
        }
    }

 
</script>

<style>
    .categorySelector {
        width: 85%;
        margin-left: auto;
        margin-right: auto;
    }
</style>
