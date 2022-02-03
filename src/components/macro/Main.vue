<template>
  <main>

        <Searchbar @search="getResults"/>

        <div v-if="!emptyKey" class="cards-media">
            <Media :type="mediaType" v-for="(item, index) in media" :key="index" :media-data="item"/>
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
                media: [],
                apiURLBase: "https://api.themoviedb.org/3/search",
                mediaType: "movie",
                authKey: "e7f8c131c7e047b16f4fcfd95ffecae2",
                loading: true,
                emptyKey: false,
            }
        },
        methods: {
            getResults(searchKey, lang="it-IT") {
                
                console.log("searchKey", searchKey);
                if (!searchKey){ 
                    this.emptyKey = true;
                    return;
                }

                axios
                    .get(this.apiURLBase + "/"+this.mediaType, 
                    {
                        params: {
                            api_key: this.authKey,
                            query: searchKey,
                            lang: lang,
                            include_adult: false,
                        }
                    })
                    .then((success) => {
                        this.media = success.data.results;
                        console.log("media", this.media);
                        this.loading = false;

                    })
                    .catch((error) => {
                        console.log(error);                        
                    })      
                                           
            }
        },

    }
</script>

<style>

</style>