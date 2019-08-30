<template>
    <div id="app">
<!--        <div id="nav">-->
<!--            <router-link to="/">Home</router-link>-->
<!--            |-->
<!--            <router-link to="/about">About</router-link>-->
<!--        </div>-->
        <router-view @play-url="playTrack"/>
        <vue-plyr ref="plyr" class="player" id="player">
            <audio></audio>
        </vue-plyr>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                playUrl: ''
            }
        },
        methods: {
            playTrack(url) {
                // this.player.stop()
                this.player.source = {
                    type: 'audio',
                    sources: [
                        {
                            src: url,
                            type: 'audio/mp3',
                        },
                    ],
                };
                this.player.play()
            }
        },
        computed: {
            player() {
                return this.$refs.plyr.player
            }
        },
        mounted() {
            // this.player.on('event', () => console.log('event fired'))
        }
    }
</script>

<style>
    body {
        padding: 0;
        margin: 0;
    }

    /*#app {*/
    /*  font-family: 'Avenir', Helvetica, Arial, sans-serif;*/
    /*  -webkit-font-smoothing: antialiased;*/
    /*  -moz-osx-font-smoothing: grayscale;*/
    /*  text-align: center;*/
    /*  color: #2c3e50;*/
    /*}*/
    /*#nav {*/
    /*  padding: 30px;*/
    /*}*/

    /*#nav a {*/
    /*  font-weight: bold;*/
    /*  color: #2c3e50;*/
    /*}*/

    /*#nav a.router-link-exact-active {*/
    /*  color: #42b983;*/
    /*}*/

    .plyr__progress__container {
        flex-grow: 2;
    }

    .player {
        position: absolute;
        bottom: 0;
        width: 100%;
    }
</style>
