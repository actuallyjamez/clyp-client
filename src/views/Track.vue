<template>
  <v-app>
    <v-card flat>
      <v-toolbar
        color="#3cbdb1"
        dark
        extended
        flat
      >
        <v-app-bar-nav-icon @click="$router.back()">
          <v-icon>mdi-arrow-left</v-icon>
        </v-app-bar-nav-icon>
      </v-toolbar>

      <v-card
        class="mx-auto"
        max-width="700"
        style="margin-top: -64px;"
      >
        <v-toolbar flat>
          <v-toolbar-title>{{trackData.Title}}</v-toolbar-title>

          <div class="flex-grow-1">
            <!--            <v-card-text>-->
            <!--              {{trackData.Title}}-->
            <!--            </v-card-text>-->
          </div>
          <v-btn fab icon @click="$emit('play-url', trackData.Mp3Url)">
            <v-icon>mdi-play</v-icon>
          </v-btn>
          <v-btn icon>
            <v-icon>mdi-dots-vertical</v-icon>
          </v-btn>
        </v-toolbar>

        <v-divider></v-divider>
        <v-card-text>
          {{trackData.Description}}
        </v-card-text>
        <v-chip-group
          multiple
          column
          active-class="primary--text"
        >
        </v-chip-group>
        <v-divider></v-divider>

        <v-card-title>Comments ({{trackComments.TotalCount}})</v-card-title>

        <div id="comments">
          <v-list-item two-line v-bind:key="comment.Comment.CommentId"
                       v-for="comment in trackComments.Data">
            <v-list-item-content>
              <v-list-item-title>{{comment.Comment.Content}}</v-list-item-title>
              <v-list-item-subtitle>{{comment.Comment.User.FirstName}}</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </div>

      </v-card>
    </v-card>
  </v-app>
</template>

<script>
    import axios from 'axios';

    export default {
        name: 'Track',
        data() {
            return {
                trackData: {},
                trackComments: {},
            };
        },
        mounted() {
            axios
                .get(`https://cors-anywhere.herokuapp.com/https://api.clyp.it/${this.$route.params.id}`)
                .then(response => (this.trackData = response.data));
            axios
                .get(`https://cors-anywhere.herokuapp.com/https://api.clyp.it/${this.$route.params.id}/comments`)
                .then(response => (this.trackComments = response.data));
        },
    };
</script>

<style scoped>
  #comments {
    margin-left: 15px;
  }
</style>
