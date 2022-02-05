<template>
  
    <div class="searchbar">

        <input type="text" class="title" v-model.trim="inputValue" placeholder="titolo del media">
        <button type="submit" @click="$emit('search', inputValue)">Cerca</button>
    </div>
</template>

<script>
    export default {
        name: 'Searchbar',
        data() {
            return {
                inputValue: ""
            }
        }
    }
</script>

<style>

</style>