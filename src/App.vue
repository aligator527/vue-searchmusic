<template>
  <div id="app">
    <div class="container">
      <div class="mx-auto my-5 display-1 text-center justify-content-center">
        SearchMusic
      </div>
      <div class="input-group mx-auto my-5 justify-content-center">
        <div class="col-8">
          <label for="search"/>
          <input title="Input song's name" id="search" class="form-control" type="text" v-model="searchText">
        </div>
      </div>
      <div>

      </div>
      <div v-for="(index) in data" v-bind:key="index" class="col-8 mx-auto my-1 justify-content-center">
        <div id="audio" class="player-wrapper">
          <div class="container-fluid">
            <div class="row">
              <div class="col-12">
                <aplayer :music="{
                  title: index.title,
                  artist: index.artist.name,
                  src: index.preview,
                  pic: index.artist.picture_medium,
                }" />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
import axios from 'axios'
import aplayer from 'vue-aplayer'

export default {
  name: 'app',
  data: function() {
    return {
      searchText: '',
      data: [],
    }
  },
  watch: {
    searchText: function() {
      if(this.searchText !== '') {
        axios.get('https://api.deezer.com/search?q=' + this.searchText).then(response => {
          // eslint-disable-next-line no-console
          console.log(response.data.data);
          this.data = response.data.data;
        })
      }
    },
  },
  methods: {

  },
  components: {
    aplayer
  }
}
</script>

<style>

</style>
