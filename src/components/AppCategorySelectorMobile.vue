<template>
    <div>
        <h3>MOBILE</h3>
        <div class="mobileMenu">
            <multiselect 
                v-model="value" 
                :options="options"
                :close-on-select="false"
                :multiple="true"
            ></multiselect>
        </div>
    </div>
</template>

<script>
    // Mobile category selection component using the vue-multiselect node module
    import Multiselect from 'vue-multiselect'

    export default {
        name: 'app-category-selector-mobile',
        props: ['options'],
        components: { Multiselect },
        data: function(){
            return {
                value: '',
            }
        }
    }
</script>

<!-- This is the css that came with the module -->
<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>