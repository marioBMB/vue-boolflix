<template>
  <section class="type">
    <h3 v-if="loaded" class="title">{{ title }}</h3>

    <ul class="card media" v-for="(item, index) in mediadata" :key="index">
      <li class="num"></li>
      <li>
        <h3>{{ item.title }}</h3>
      </li>
      <li>{{ item.original_title }}</li>
      <li>
        <img class="flag" :src="require(`../../assets/img/${getFlagName(item.original_language)}`)"/>
      </li>
      <li>
          <i v-for="star in getStars(item.vote_average)" :key="`piena${star}`" class="fas fa-stars"></i>
          <i v-for="star in (5 - getStars(item.vote_average))" :key="`vuota${star}`" class="far fa-stars"></i>
      </li>
      <li><img class='poster' :src="imgsrc + item.poster_path" /></li>
    </ul>
  </section>
</template>

<script>
export default {
  name: "Media",
  props: {
    mediadata: Array,
    title: String,
    type: String,
    imgsrc: String,
  },
  data() {
    return {
      imgRelPathFolder: "../../assets/img/",
      loaded: false,
    };
  },
  methods: {

    getStars(vote){

        return Math.ceil(vote / 2);
    },  
    getFlagName(lang) {
      let img = "unknown.jpg";

      if (this.imgExists(lang, ".gif")) {
        img = lang + ".gif";
      }
      return img;
    },
    imgExists(name, ext) {
      // return ['it', 'en'].includes(name);

      try {
        require(`../../assets/img/${name}${ext}`);
        return true;
      } 
      catch (error) {
        return false;
      }
    },
  },
  created() {
    console.log("mediadata", this.mediadata);
    // this.loaded = (this.mediadata.length > 0);
  },
};
</script>

<style lang="scss" scoped>
    section {
    width: 100%;
    margin: 2rem 0;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;

    .title {
        width: 100%;
        margin: 2rem;
    }

    .poster {
        width: 100%;
        height: auto;

            img {
                width: 100%;
            }
    }
    }
    .flag {
    width: 25px;
    height: 15px;
    object-fit: cover;
    }
</style>