<template>
  <header>
      <div class="container">

        <a href="#">
            <div class="main-logo">
                <img src="https://gogomagazine.it/wp-content/uploads/2020/01/cinema-4153289_640-560x412.jpg" alt="">
            </div>
            <h3>Boolflix</h3>
        </a>

        <Searchbar @search="propagateEvent"/>
      </div>
  </header>
</template>

<script>

    import Searchbar from "../commons/Searchbar.vue";

    export default {
        name: 'Header',
        components: {
            Searchbar,
        },
        methods: {
            propagateEvent(inputValue){
                this.$emit('listen_search', inputValue);
            }
        }
    }
</script>

<style lang="scss" scoped>


    header {
   
        width: 100%;
        height: 80px;
        background-color: #333;
        color: black;

        .container {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 30% 0 2rem; 
        }

        a {
            display: flex;
            align-items: center;
            text-decoration: none;
        }
        .main-logo {
            height: 100%;
            padding: 10px;

            img {
                height:100%;
                width: 80px;
                border-radius: 10px;
            }
        }
        h3 {
            color: rgb(153, 0, 0);
            text-transform: uppercase;
        }
        
    }
</style>