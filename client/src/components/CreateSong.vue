<template>
  <v-layout>
    <v-flex xs4>
      <panel title="Song Metadata">
        <v-text-field
            append-icon="star"
            v-model="song.title"
            label="Title"
            required
            :rules="[rules.required]"
        ></v-text-field>

        <v-text-field
            append-icon="star"
            v-model="song.artist"
            label="Artist"
            required
            :rules="[rules.required]"
        ></v-text-field>

        <v-text-field
            append-icon="star"
            v-model="song.genre"
            label="Genre"
            required
            :rules="[rules.required]"
        ></v-text-field>

        <v-text-field
            append-icon="star"
            v-model="song.album"
            label="Album"
            required
            :rules="[rules.required]"
        ></v-text-field>

        <v-text-field
            append-icon="star"
            v-model="song.albumImage"
            label="Album Image Url"
            required
            :rules="[rules.required]"
        ></v-text-field>

        <v-text-field
            append-icon="star"
            v-model="song.youtubeId"
            label="YouTube ID"
            required
            :rules="[rules.required]"
        ></v-text-field>
      </panel>
    </v-flex>

    <v-flex xs8>
      <panel title="Song Structure" class="ml-4">
        <v-text-field
            append-icon="star"
            v-model="song.tab"
            label="Tab"
            multi-line
            required
            :rules="[rules.required]"
            ></v-text-field>

          <v-text-field
            append-icon="star"
            v-model="song.lyrics"
            label="Lyrics"
            multi-line
            required
            :rules="[rules.required]"
        ></v-text-field>
      </panel>

      <div class="danger-alert" v-if="error">
        {{error}}
      </div>

      <div class v-else>
        <v-icon>star</v-icon>Required Fields
      </div>

      <v-btn
        dark
        color="primary"
        @click="create">
        Create Song
      </v-btn>
    </v-flex>
  </v-layout>
</template>

<script>
import Panel from '@/components/Panel'
import SongService from '@/services/SongsService'
export default {
  data () {
    return {
      song: {
        title: null,
        artist: null,
        genre: null,
        album: null,
        albumImage: null,
        youtubeId: null,
        lyrics: null,
        tab: null
      },
      error: null,
      rules: {
        required: (value) => !!value || 'Required'
      }
    }
  },
  methods: {
    async create () {
      this.error = null

      const areAllFieldsFilledIn = Object
        .keys(this.song)
        .every(key => !!this.song[key])

      if (!areAllFieldsFilledIn) {
        this.error = 'Please fill in the required fields'
        return
      }
      try {
        await SongService.post(this.song)
        this.$router.push({
          name: 'songs'
        })
      } catch (err) {
        console.log(err)
      }
    }
  },
  components: {
    Panel
  }
}
</script>
<style scoped>
</style>
