<template>
    <div class="card-grid">
          <p v-if="cardData.length < 1" class="no-card-data-found">
              No card data loaded.
            </p>
        <div class="card--body" v-for="card in cardData" :key="card.id">
          <img :src="card.image" v-bind:alt="`${ card.title }`">
          <p class="card--body__title">{{ card.title }}</p>
          <p class="card--body__description">{{ card.description | truncate(200, '...') }}</p>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'app-cards',
        props: {
            cardData: Array
        },
        data() {
            return {}
        },
        methods: {

        },
        filters: {
            truncate: function (text, length, suffix) {
                return text.substring(0, length) + suffix
            },
        },
    }
</script>

<style scoped>
    .card-grid {
        font-family: Arial, Helvetica, sans-serif;
        color: #000;
        text-align: center;
    }

    .card--body {
        height: 280px;
        width: 215px;
        border: 1px solid #f00;
        overflow: hidden;
    }

    .card--body__title {
        font-size: 1em;
        font-weight: 700;
    }

    .card--body__description {
        font-size: .75em;
        text-align: left;
        overflow: hidden;
        hyphens: auto;
        text-overflow: ellipsis;
        margin: 10px;
        line-clamp: 6;
        -webkit-line-clamp: 6;
    }


    img {
        height: 100px;
    }
</style>