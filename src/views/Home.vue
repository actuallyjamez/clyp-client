<template>
  <div class="home">
    <ul>
      <li class="clickable" v-bind:key="item.AudioFileId" v-for="item in featured" @click="play(item.Mp3Url)">{{item.Title}} - {{item.User.FirstName}}</li>
    </ul>
  </div>
</template>

<script>
    // @ is an alias to /src

    import axios from "axios"

    export default {
        name: 'home',
        data() {
            return {
                featured: {}
            }
        },
        methods: {
            play(url){
                this.$emit('play-url', url)

            }
        },
        mounted() {
            axios
                .get('https://cors-anywhere.herokuapp.com/https://api.clyp.it/FeaturedList/Featured')
                .then(response => (this.featured = response.data))
        }
    }
</script>

<style>
    .clickable {
        cursor: pointer;
    }
    .clickable:hover{
        text-decoration: underline;
    }
</style>
