<template>
    <div class="categorySelector">
        <div v-if="isMobile">
            <app-category-selector-mobile :options="options" />
        </div>
        <div v-else>
            <app-category-selector-desktop :options="options" />
        </div>
    </div>
</template>

<script>
    /* 
        This "controller" manages the the two application category selectors,
        one for mobile and one for desktop.  It was getting too hairy to manage all in one place, especially with the mobile and DTP functionality being different.

        This also means only one place to send the data.
    */
    import { isMobile } from 'mobile-device-detect'
    import AppCategorySelectorDesktop from '@/components/AppCategorySelectorDesktop.vue'
    import AppCategorySelectorMobile from '@/components/AppCategorySelectorMobile.vue'
    
    export default {
        name: 'app',
        
        components: {
            AppCategorySelectorMobile,
            AppCategorySelectorDesktop,
        },
        data: function() {
            // This could optionally be populated from REST or whatever
            return {
                isMobile: isMobile,
                options: ['AEM', 'ANALYTICS', 'UX', 'INFORMATION ARCHITECTURE', 'VISUAL DESIGN', 'SITECORE', 'CX STRATEGY', 'ADOBE DAM', 'TAXONOMY', 'PHOTOGRAPHY', 'ADOBE ANALYTICS'],
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
