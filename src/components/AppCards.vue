<template>
    <div class="card-grid">
        <p v-if="cardData.length < 1" class="no-card-data-found">
              No card data loaded.
        </p>
            <div  v-if="filterList.length > 0">
            <div
            class="card--body selected-cards" 
            v-for="(card, index) in cardsToShow"
            :key="index"
            >
            <img :src="card.image" v-bind:alt="`${ card.title }`">
            <p class="card--body__title">{{ card.title }}</p>
            <p class="card--body__description">{{ card.description }}</p>
            </div>
            </div>

            <div v-else>
            <div
                class="card--body selected-cards" 
                v-for="(card, index) in cardData"
                :key="index"
            >

            <img :src="card.image" v-bind:alt="`${ card.title }`">
            <p class="card--body__title">{{ card.title }}</p>
            <p class="card--body__description">{{ card.description }}</p>
            </div>
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
                // this.$root to the rescue!
                filterKey: "tags",
                filterList: [],
            }
        },
        computed: {
            cardsToShow() {
                // A little kludgy because not exact correspondence between the
                // tags and the searchable items.

                return this.cardData.filter(card => {
                    let foo = card.tags.map(item => item.toUpperCase())
                    return (this.filterList.some(item => foo.includes(item)))
                })
            }

        },
        methods: {
            matcher: function(whichCard) {
                // NOT USED
                return (this.filterList.some(item => whichCard.includes(item)))
            }
        },
        mounted() {
            this.$root.$on('toggleapproot', (incomingFilterList) => {
                this.filterList = incomingFilterList
            })
        },

        filters: {            
            // selectedCards: function(arr1, arr2) {
            //     return (arr2.some(item => arr1.includes(item)))
            // },

            truncate: function (text, length, suffix) { // not used
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