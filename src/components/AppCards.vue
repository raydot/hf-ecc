<template>
    <div class="card-grid">
          <p v-if="cardData.length < 1" class="no-card-data-found">
              No card data loaded.
        </p>
        <div class="card--body" v-for="card in cardData" :key="card.id">
          <img :src="card.image" v-bind:alt="`${ card.title }`">
          <p class="card--body__title">{{ card.title }}</p>
          <p class="card--body__description">{{ card.description }}</p>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'app-cards',
        props: {
            cardData: Array,
        },
        data: function() {
            return {

            }
        },
        methods: {

        },
        filters: {
            truncate: function (text, length, suffix) {
                return text.substring(0, length) + suffix
            },
            /* usage: {{ text | truncate(250, '...') }}  Interesting approach, but probably not the best */
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
        margin:10px;
        float: left;
        border: 1px solid #f00;
        overflow: hidden;
    }

    .card--body__title {
        font-size: 1em;
        font-weight: 700;
    }

    .card--body__description {
        margin: 10px;
        font-size: .75em;
        text-align: left;
        overflow: hidden;
        position: relative;
        line-height: 1.2em;
        max-height: 7em;
        /* margin-right: -1em; */
        padding-right: 1em;
    }

    .card--body__description:before {
        content: '...';
        position: absolute;
        right: 1em; 
        background-color: #fff;
        bottom: 0;
    }

    .card--body__desciption:after {
        content: '';
        position: absolute;
        right: 0;
        width: 1em;
        height: 1em;
        margin-top: 0.2em;
        background: #fff;
    }


    img {
        height: 100px;
    }
</style>