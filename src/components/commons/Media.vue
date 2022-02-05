<template>
    <section class='type'>   
        <h3 v-if="loaded" class='title'>{{title}}</h3>

        <ul class='card media' v-for="(item,index) in mediaData" :key="index">
            <li class="num"></li>  
            <li><h3>{{item.title}}</h3></li>
            <li>{{item.original_title}}</li>
            <li><img class='flag' :src="require(`../../assets/img/${getFlagName(item.original_language)}`)"></li>
            <li>{{item.vote_average}}</li>
        </ul>
    </section>
</template>

<script>
    export default {
        name: "Media",
        props: {
            mediaData: Array,
            title: String,
            type: String,
        },
        data() {
            return {

                imgRelPathFolder: "../../assets/img/",
                loaded: false,
            }
        },
        methods: {
            getFlagName(lang){

                let img = "unknown.jpg";
       
                if (this.imgExists(lang, ".gif")){
                    img = lang+".gif";
                }
                return img;
            },
            imgExists(name, ext){
                // return ['it', 'en'].includes(name);

                try {
                    require(`../../assets/img/${name}${ext}`);
                    return true;
                }
                catch(error){
                    return false;
                }
            },
        },
        updated() {
            this.loaded = (this.mediaData.length > 0);
        }
    }
    
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
    }
    .flag {
        width: 25px;
        height: 15px;
        object-fit: cover;
    }
</style>