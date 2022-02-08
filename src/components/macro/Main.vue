<template>
    <main>

        <h3>{{message}}</h3>
        <div v-if="searchkey != ''" class="cards-container">
            <Media type='movie' :mediadata="datalist.movie[0]" title="Film" :imgsrc="baseimgURL" />
            <Media type='tv' :mediadata="datalist.tv[0]" title="Serie Tv" :imgsrc="baseimgURL" />
        </div>
        <div v-else>La chiave di ricerca non può essere vuota</div>
    </main>
</template>

<script>
    import Media from "../commons/Media.vue";

    export default {
        name: "Main",
        components: {
            Media,
        },
        props: {
            datalist: Object,
            searchkey: String
        },
        data() {
            return {
                movies: [],
                tvseries: [],
                loading: true,
                message: "",
                baseimgURL: "https://image.tmdb.org/t/p/w342",
            }
        },
        methods: {
          
        },
        updated() {
            console.log("datalist", this.datalist);
        }
    }
</script>

<style lang="scss">

    .cards-container {
        display: flex;
        flex-wrap: wrap;
        align-items: center;
        justify-content: center;


        .card.media {
            
            background-size: 100% 100%;
            background-repeat: no-repeat;
            background-position: center;
            margin: 20px;
            list-style: none;
            border: 1px solid #555;
            width: 200px;
            height: 300px;
            overflow-y: auto;

            font-size: 0.8rem;
            
            li {
                margin: 10px;
            }

        }
    }
</style>