<template>
    <div id="app" class="foo">
      <h1>Test Results</h1>
      <app-cards :cardData="cardData" />
    </div>
</template>

<script>
  import AppCards from '@/components/AppCards.vue'

  export default {
    name: 'app',
    components: {
      AppCards,
    },
    data() {
      return {
        cardData: []
      }
    },
    mounted() {
      this.getCards()
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
