

<template>
    <div>
        <div class="mobileMenu" v-if="isMobile">
            <multiselect v-model="value" :options="options"></multiselect>
        </div>
        <div class="desktopMenu--items" v-else>
            <span 
                v-for="option in options" 
                v-bind:key="option" 
                v-on:click="handleClick" 
                v-bind:class="{ active: isActive }">
                    {{ option }}
                </span>
        </div>
    </div>
</template>

<script>

    /*
        This component was doing way too much and has been split up into three components.

        AppCategorySelector
            |- AppCategorySelectorDesktop
            |- AppCategorySelectorMobile

        This component is no longer in use.
    */


    import Multiselect from 'vue-multiselect'
    export default {
        name: 'app-mobile-select',
        components: { Multiselect },
        data: {
            active: true,
            //return {
                value: null,
                isMobile: false,
                options: ['AEM', 'ANALYTICS', 'UX', 'INFORMATION ARCHITECTURE', 'VISUAL DESIGN', 'SITECORE', 'CX STRATEGY', 'ADOBE DAM', 'TAXONOMY', 'PHOTOGRAPHY', 'ADOBE ANALYTICS'],
            //}
        },
        methods: {
            handleClick: function(event) {
                console.log(event.target)
            },

            

        },
    }
</script>


<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>
<style>
    .desktopMenu {
        width: 85%;
    }  
    .desktopMenu--items {
        display: inline-block;
        color: #000;
        font-family: Arial, Helvetica, sans-serif;
        font-size: .85em;
        border: 1px #000 solid;
        margin: .2em;
        padding: .2em;
    }
  
</style>

