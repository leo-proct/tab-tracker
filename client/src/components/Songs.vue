<template>
  <v-layout row>
    <v-flex xs6 offset-xs3>
      <panel title ="Songs">
        <v-btn
          slot="action"
          @click="navigateTo({name: 'songs-create'})"
          color="success"
          medium
          absolute
          right
          middle
          fab>
          <v-icon>add</v-icon>
        </v-btn>

        <div v-for="song in songs"
          :key="song.id"
          class='song'>
          <v-layout row>
            <v-flex xs6>
              <div class="song-title">
                 {{song.title}}
              </div>
              <div class="song-artist">
                 {{song.artist}}
              </div>
              <div class="song-genre">
                 {{song.genre}}
              </div>

              <v-btn
                dark
                color="primary"
                @click="navigateTo({
                  name: 'song',
                   params: {songId: song.id}
                   })">
                View
              </v-btn>
            </v-flex>

            <v-flex xs6>
              <img class="album-image" :src="song.albumImage" />
            </v-flex>
          </v-layout>
        </div>
      </panel>
    </v-flex>
  </v-layout>
</template>

<script>
import SongsService from '@/services/SongsService'
import Panel from '@/components/Panel'
export default {
  components: {
    Panel
  },
  data () {
    return {
      songs: null
    }
  },
  methods: {
    navigateTo (route) {
      this.$router.push(route)
    }
  },
  async mounted () {
    // do a request for songs
    this.songs = (await SongsService.index()).data
  }
}

</script>
<style scoped>
.song{
  padding: 20px;
  height: 20%;
  overflow: hidden;
}
.album-image {
  width: 50%;
  margin: 0 auto;
}
.song-title{
  font-size: 30px;
}
.song-artist{
  font-size: 24px;
}
.song-genre{
  font-size: 18px;
}
</style>
