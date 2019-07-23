<template>
    <div id="app" class="foo">
      <h1>Test Results</h1>
      <div>
          <app-category-selector v-on:updateSelection="updateSelection" />
      </div>
      <app-cards :cardData="cardData" />
    </div>
</template>

<script>
  import AppCategorySelector from '@/components/AppCategorySelector.vue'
  import AppCards from '@/components/AppCards.vue'

  export default {
    name: 'app',
    components: {
      AppCards,
      AppCategorySelector,
    },
    data() {
      return {
        cardData: [],
      }
    },
    mounted() {
      this.getCards()
    },
    methods: {
      // Fetch JSON data from source.
      async getCards() {
        try {
          const response = await fetch('https://s3-us-west-1.amazonaws.com/hero-engineering-public/interview/fe-code-challenge.json')
          const data = await response.json()
          this.cardData = data.cards
        } catch(error) {
          alert(error) // Or somehow handle the error.
        }
      },
      updateSelection() {
        alert('UPDATE!')
      }
    }
  }
</script>

<style lang="scss">

</style>
