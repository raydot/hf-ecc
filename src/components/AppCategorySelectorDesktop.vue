<template>
    <div class="desktopMenu--items">
        <h3>DESKTOP</h3>
        <span
            v-for="option in options"
            v-bind:key="option"
        >
            <app-category-selector-desktop-button :option="option" v-on:toggleprop="toggleprop" />
        </span>
    </div>
</template>

<script>
    // Desktop category selection component

    import AppCategorySelectorDesktopButton from '@/components/AppCategorySelectorDesktopButton.vue'

    export default{
        name: 'app-category-selector-desktop',
        components: {
            AppCategorySelectorDesktopButton
        },
        props: ['options'],
        data: function() {
            return {
                
            }  
        },
        events: {
            toggleprop: function(whichProp) {
                alert(whichProp)
            }
        } 
    }
</script>

<style> 
    
</style>