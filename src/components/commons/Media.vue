<template>
  
    <ul>
        <li>{{mediaData.title}}</li>
        <li>{{mediaData.original_title}}</li>
        <li>{{mediaData.original_language}}</li>
        <li>{{mediaData.vote_average}}</li>
    </ul>
</template>

<script>
    export default {
        name: "Media",
        props: {
            mediaData: Object
        }
    }
</script>

<style>

</style>