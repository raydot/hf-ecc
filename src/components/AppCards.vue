<template>
    <div class="card-grid">
        <div v-if="cardData.length < 1" class="no-card-data-found">
            <p>
                No card data loaded.
            </p>
        </div>
        <div v-else-if="filterList.length > 0">
            <div
                class="card--body selected-cards flip-card" 
                v-for="(card, index) in cardsToShow"
                :key="index"
            >
                <div class="flip-card--inner">
                    <div class="flip-card__front parent">
                        <img :src="card.image" v-bind:alt="`${ card.title }`" />
                        <p class="card--body__title">{{ card.title }}</p>
                        <p class="card--body__description">{{ card.description }}</p>
                    </div>
                    <div class="flip-card__back parent">
                        <div class="img-placeholder">&nbsp;</div>
                        <h3>{{ card.id }}</h3>
                        <p 
                            v-for="(tag, index) in card.tags"
                            :key = "index"
                            class="tag-list"
                        >
                            <span class="card-tag">
                                {{ tag }}
                            </span>
                        </p>
                    </div>
                </div>
            </div>
        </div>
        <div v-else>
<div
                class="card--body selected-cards flip-card" 
                v-for="(card, index) in cardData"
                :key="index"
            >
                <div class="flip-card--inner">
                    <div class="flip-card__front parent">
                        <img :src="card.image" v-bind:alt="`${ card.title }`" />
                        <p class="card--body__title">{{ card.title }}</p>
                        <p class="card--body__description">{{ card.description }}</p>
                    </div>
                    <div class="flip-card__back parent">
                        <div class="img-placeholder">&nbsp;</div>
                        <h3>{{ card.id }}</h3>
                        <p 
                            v-for="(tag, index) in card.tags"
                            :key = "index"
                            class="tag-list"
                        >
                            <span class="card-tag">
                                {{ tag }}
                            </span>
                        </p>
                    </div>
                </div>
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
        /* border: 1px solid #f00; */
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

    .card-tag {
        float: left;
        font-size: .75em;
        background-color: #000;
    
        color: white;
        padding: .25em;
        margin: .25em;
    }

    img {
        height: 100px;
        background-color: transparent;
    }

    .img-placeholder {
        background-color: transparent;
        height: 100px;
    }

      /* RIBBON */
    .parent {
        overflow: hidden; /* required */
        width: 50%; /* for demo only */
        height: 250px /* some non-zero number */;
        margin: 25px auto; /* for demo only */
        border:1px solid grey; /* for demo only */
        position: relative; /* required  for demo */
    }

    .ribbon {
        margin: 0;
        padding: 0;
        background: #333;
        color:white;
        font-family: Arial, Helvetica, sans-serif;
        font-size: 0.85em;
        font-style: italic;
        padding:0.33em 0;
        position: absolute;
        top:0;
        right:0;
        transform: translateX(30%) translateY(0%) rotate(45deg);
        transform-origin: top left;
    }
    .ribbon:before,
    .ribbon:after {
        content: '';
        position: absolute;
        top:0;
        margin: 0 -1px; /* tweak */
        width: 100%;
        height: 100%;
        background: #333;
    }
    .ribbon:before {
        right:100%;
    }

    .ribbon:after {
        left:100%;
    }

    /* Flip Card CSS */

    /* Flip card container */
    .flip-card {
        /* background-color: transparent; */
        background-color: #fff;
        height: 280px;
        width: 215px;
        border: 1px solid #f1f1f1;
        perspective: 1000px; /* Remove this if you don't want the 3D effect */
    }
    
    /* position the front and back side */
    .flip-card--inner {
        position: relative;
        width: 100%;
        height: 100%;
        text-align: center;
        transition: transform 0.8s;
        transform-style: preserve-3d;
    }
    
    /* Do an horizontal flip when you move the mouse over the flip box container */
    /* Needs to be tap for mobile */
    .flip-card:hover .flip-card--inner {
        transform: rotateY(180deg);
    }
    
    /* Position the front and back side */
    .flip-card__front, .flip-card__back {
        position: absolute;
        width: 100%;
        height: 100%;
        backface-visibility: hidden;
    }
    
    /* Style the front side  */
    .flip-card__front {
        background-color: #fff;
        color: black;
    }
    
    /* Style the back side */
    .flip-card__back {
        /* background-color: dodgerblue; */
        color: black;
        transform: rotateY(180deg);
    }
</style>