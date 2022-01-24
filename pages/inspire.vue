<template>
  <v-row>
    <v-col class="text-center">
      <img
        src="/v.png"
        alt="Vuetify.js"
        class="mb-5"
      >
      <v-spacer />
      <v-list>
        <v-list-item v-for="gif in listGif" :key="gif.id">
          <v-list-item-content class="justify-center">
            <v-list-item-title>
              <a :href="gif.url" target="_blank">
                {{ gif.title }}
              </a>
            </v-list-item-title>
            <v-img :src="gif.images.fixed_height_small.url" aspect-ratio="1" max-width="200px" height="200px"/>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-col>
  </v-row>
</template>

<script lang="ts">
import Vue from 'vue'

const API_URL = 'https://api.giphy.com/v1/gifs/search?api_key=X6InBQzbNibdbpGg2XKct0lYBDj9SGNJ&q=padawan&rating=g'

export default Vue.extend({
  async asyncData({ $axios }) {
    const response =  await $axios.get(API_URL)
    if (response) {
      return {
        listGif: response.data.data
      }
    }
    return { listGif: [] }
  },
})
</script>