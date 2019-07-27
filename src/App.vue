<template>
    <div id="app" class="foo">
      <h1>Test Results</h1>
      <div>
          <app-category-selector :options="options"/>
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
        cardData: [], // hold the list of cards
        options: ['AEM', 'ANALYTICS', 'UX', 'INFORMATION ARCHITECTURE', 'VISUAL DESIGN', 'SITECORE', 'CX STRATEGY', 'ADOBE DAM', 'TAXONOMY', 'PHOTOGRAPHY', 'ADOBE ANALYTICS'], // set / hold the selection options
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
      // toggleapp(filterList) {
      //   alert('xx', filterList)
      // },
    }
  }
</script>

<style lang="scss">

</style>
