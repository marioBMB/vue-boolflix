<template>
  <main>

        <Searchbar @search="getResults"/>

        <h3>{{message}}</h3>
        <div v-if="!emptyKey" class="cards-container">
            <Media type='movie' :media-data="media.movie[0]" title="Film"/>
            <Media type='tv' :media-data="media.tv[0]" title="Serie Tv"/>
        </div>
        <div v-else>La chiave di ricerca non può essere vuota</div>
  </main>
</template>

<script>

    import axios from 'axios';
    import Searchbar from "../commons/Searchbar.vue";
    import Media from "../commons/Media.vue";

    export default {
        name: "Main",
        components: {
            Searchbar,
            Media,
        },
        data() {
            return {
                media: {
                    movie: [],
                    tv: [],
                },
                apiURLBase: "https://api.themoviedb.org/3/search",
                authKey: "e7f8c131c7e047b16f4fcfd95ffecae2",
                loading: true,
                emptyKey: false,
                message: "",
                mediaCounter: 0,
            }
        },
        computed:{
        },
        methods: {

            getResults(searchKey) {

                this.media = {
                    movie: [],
                    tv: [],
                };
                this.searchMedia(searchKey, "movie");
                this.searchMedia(searchKey, "tv");

                console.log(this.media.movie);
                console.log(this.media.tv);

            },
            searchMedia(searchKey, mediaType, lang="it-IT") {

                console.log("searchKey",searchKey)
                console.log("mediaType",mediaType)
                console.log("lang",lang)

                
                if (!searchKey) { this.emptyKey = true; return; }  
                
                axios
                    .get(this.apiURLBase + "/"+ mediaType, 
                    {
                        params: {
                            api_key: this.authKey,
                            query: searchKey,
                            lang: lang,
                            include_adult: false,
                        }
                    })
                    .then((success) => {    

                        this.mediaCounter++;
                        this.media[mediaType].push(success.data.results);
                        if (mediaType == 'tv'){
                            this.formatFields(mediaType);
                        }

                        if (this.mediaCounter == Object.keys(this.media).length){
                            this.loading = false;
                            this.message = "Risultati di ricerca:";
                        }
                    })
                    .catch((error) => {
                        console.log(error);                        
                    })                                    
            },

            formatFields(mediaType){

                const arrayModObj = [];

                this.media[mediaType][0].forEach((elem) => {
                    const objApp = {
                        title: elem.name,
                        original_title: elem.original_name,
                        language: elem.language,
                        vote_average: elem.vote_average,
                    };
                    arrayModObj.push(objApp);
                });
                this.media[mediaType][0] = arrayModObj;
            }
          
        },

    }
</script>

<style lang="scss">

    .cards-container {
        display: flex;
        flex-wrap: wrap;
        align-items: center;
        justify-content: center;


        .media {

            list-style: none;
            margin: 20px;
            border: 1px solid #555;

            width: 200px;
            height: 200px;
            padding: 10px 20px;
            overflow-y: auto;

            font-size: 0.8rem;
            
            li {
                margin: 10px;
            }

        }
    }
</style>