<template>
        <span
            class="desktopMenu--items"
            v-bind:class="{ active: isActive }"
            @click="handleClick"
        >
            {{ option }}
        </span>
</template>

<script>
    // This might be overkill, but I was having trouble keeping the data separate
    // while creating the buttons in the component that displays them.
    // This also solves the problem of having to query the html for the button value.  
    // Bonus: reusable!
    export default {
        name: 'app-category-selector-desktop-button',
        props: ['option'],
        data: function() {
            return {
                isActive: false,
            }  
        },
        methods: {
            handleClick: function() {
                // Toggle the click and emit values to AppCategorySelector
                this.isActive = !this.isActive
                this.$emit('toggleprop', this.option)
            }
        }
    }
</script>

<style>
    .desktopMenu--items {
        display: inline-block;
        color: #000;
        background-color: #fff;
        font-family: Arial, Helvetica, sans-serif;
        font-size: .85em;
        border: 1px #000 solid;
        margin: .2em;
        padding: .2em;
    }

    .desktopMenu--items .active {
        color: #fff;
        background-color: #000;

    }
</style>