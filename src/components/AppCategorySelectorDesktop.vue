<template>
    <div class="desktopMenu--items">
        <span
            v-for="(option, index) in options"
            :option="option"
            :key="index"
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
        methods: {
            // Admittedly, double-emit from grandchild to grandparent isn't ideal,
            // but Vuex seems like overkill.
            // OOF!  I realized I can just use $root after I set this up.
            toggleprop(whichProp) {
                this.$emit('toggleprop', whichProp)
            }
        } 
    }
</script>

<style> 
    
</style>