<template>
    <div id="app" class="foo">
      <h1>Test Results</h1>
      <div>
          <app-category-selector />
      </div>
      <app-cards :cardData="cardData" />
    </div>
</template>

<script>
  import AppCategorySelector from '@/components/AppCategorySelector.vue'
  import AppCards from '@/components/AppCards.vue'
  //import AppMobileSelect from '@/components/AppMobileSelect.vue'
  //import { isMobile } from 'mobile-device-detect'

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
      //const isMobile = isMobile
    },
    methods: {
      async getCards() {
        try {
          const response = await fetch('https://s3-us-west-1.amazonaws.com/hero-engineering-public/interview/fe-code-challenge.json')
          //const response = await fetch('https://jsonplaceholder.typicode.com/users')
          const data = await response.json()
          this.cardData = data.cards
          //console.log(this.cardData)
        } catch(error) {
          // eslint-disable-next-line
          console.error(error) // Or somehow handle the error.
        }
      },
    }
  }
</script>

<style lang="scss">

</style>
