<template>
  <div id="app">

    <Header @listen_search="updateAPIdata"/>
    <Main :datalist="media" :searchkey="userInput"/>
    <Footer />
  </div>
</template>

<script>
  import axios from 'axios';
  import Header from './components/macro/Header.vue';
  import Main from './components/macro/Main.vue';
  import Footer from './components/macro/Footer.vue';

  export default {
    name: 'App',
    components: {
      Header,
      Main,
      Footer
    },
    data(){
      return {
            media: {
                movie: [],
                tv: []
            },
            apiURLBase: "https://api.themoviedb.org/3/search",
            authKey: "e7f8c131c7e047b16f4fcfd95ffecae2",
            mediaCounter: 0,
            userInput: "",
      }
    },
    methods: {

      updateAPIdata(inputValue){

        this.userInput = inputValue;
        this.getResults(inputValue);
      },
      getResults(searchKey) {

          this.media = { movie: [], tv: [] };
          this.searchMedia(searchKey, "movie");
          this.searchMedia(searchKey, "tv");

      },
      searchMedia(searchKey, mediaType, language="it-IT") {

          console.log("searchKey",searchKey);
          console.log("mediaType",mediaType);

            if (!searchKey) { this.emptyKey = true; return; }  
                
              axios
                  .get(this.apiURLBase + "/"+ mediaType, 
                  {
                      params: {
                          api_key: this.authKey,
                          query: searchKey,
                          lang: language,
                          include_adult: false,
                      }
                  })
                  .then((success) => {    

                      this.mediaCounter++;
                      this.media[mediaType].push(success.data.results);
                      mediaType == 'tv'? this.formatFields(mediaType) : null;

                      console.log("media", this.media);

                        /* DA TRASFERIRE NEL MAIN 
                      if (this.mediaCounter == Object.keys(this.media).length){
                          this.loading = false;
                          this.message = "Risultati di ricerca:";
                      }
                      */
                  })
                  .catch((error) => {
                      console.log(error);                        
                  });                                 
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
    @import "./assets/style/globals.scss";
</style>