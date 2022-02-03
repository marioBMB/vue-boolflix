<template>
  <header>
      <div class="container">

        <div class="main-logo">
            <img src="https://gogomagazine.it/wp-content/uploads/2020/01/cinema-4153289_640-560x412.jpg" alt="">
        </div>
        <h3>Boolflix</h3>
      </div>
  </header>
</template>

<script>
    export default {
        name: 'Header',
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
            justify-content: flex-start;
            align-items: center; 
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
            color: maroon;
            text-transform: uppercase;
        }
        
    }
</style>