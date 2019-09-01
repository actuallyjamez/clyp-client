<!--<template>-->
<!--  <div class="home">-->
<!--    <ul>-->
<!--      <li class="clickable" v-bind:key="item.AudioFileId" v-for="item in featured" @click="goToTrack(item.AudioFileId)">{{item.Title}} - {{item.User.FirstName}}</li>-->
<!--    </ul>-->
<!--  </div>-->
<!--</template>-->
<template>
  <v-app>
    <v-app-bar
      color="#3cbdb1"
      dark
    >
      <v-toolbar-title>Clyp Featured</v-toolbar-title>
<!--      <div class="flex-grow-1"></div>-->
    </v-app-bar>
    <v-content style="height: 100%" >
      <v-row>
        <v-col v-bind:key="item.AudioFileId" v-for="item in featured" >
          <v-card
            class="mx-auto"
            max-width="720"
            outlined
          >
            <v-list-item three-line>
              <v-list-item-content>
                <div class="mb-4">{{item.User.FirstName}}</div>
                <v-list-item-title class="headline mb-1">{{item.Title}}</v-list-item-title>
                <v-list-item-subtitle> {{item.Description}}
                </v-list-item-subtitle>
              </v-list-item-content>

              <v-list-item-avatar
                tile
                size="80"
                color="#3cbdb1"
              >
                <v-img :src="item.ArtworkPictureUrl"></v-img>
              </v-list-item-avatar>
            </v-list-item>

            <v-card-actions>
              <v-btn text @click="play(item.Mp3Url)">Play</v-btn>
              <v-btn text @click="goToTrack(item.AudioFileId)">More Info</v-btn>
            </v-card-actions>
          </v-card>

        </v-col>
      </v-row>
    </v-content>


  </v-app>
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
            play(url) {
                this.$emit('play-url', url)
            },
            goToTrack(id) {
                this.$router.push(`/${id}`)
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

  .clickable:hover {
    text-decoration: underline;
  }
</style>
