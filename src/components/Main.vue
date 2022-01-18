<template>
  <main class="container pb-4">
    <div class="row" v-if="albums">
      <div class="col-6">
        <select v-model="selected" @change="changeChoice()">
          <option>All</option>
          <option
            v-for="(genre, index) in genres"
            :key="index + 'Genre'"
            :value="genre"
          >
            {{ genre }}
          </option>
        </select>
      </div>
    </div>
    <div class="row row-cols-6 gap-3" v-if="albums">
      <Album
        v-for="(album, index) in filteredAlbums"
        :key="index"
        :album="album"
      />
    </div>
    <div class="row loading" v-else>
      <div class="col-12">
        <h1>Loading...</h1>
      </div>
    </div>
  </main>
</template>

<script>
import axios from "axios";
import Album from "./Album.vue";

export default {
  name: "Main",
  components: {
    Album,
  },
  data() {
    return {
      albums: null,
      filteredAlbums: null,
      genres: null,
      selected: null,
      queryApi: "https://flynn.boolean.careers/exercises/api/array/music",
    };
  },
  mounted() {
    this.getAlbums();
  },
  methods: {
    getAlbums() {
      setTimeout(() => {
        axios
          .get(this.queryApi)
          .then((result) => {
            this.albums = result.data.response;
            this.getGenre();
            this.filteredAlbums = this.albums;
          })
          .catch((error) => {
            console.log(error);
          });
      }, 1000);
    },
    getGenre() {
      const genresArray = [];
      for (let i = 0; i < this.albums.length; i++) {
        const element = this.albums[i];
        while (!genresArray.includes(element.genre)) {
          genresArray.push(element.genre);
        }
      }
      this.genres = genresArray;
    },
    changeChoice() {
      if (this.selected == "" || this.selected == "All") {
        this.filteredAlbums = this.albums;
      } else {
        this.filteredAlbums = this.albums.filter((album) => {
          return album.genre == this.selected;
        });
      }
    },
  },
};
</script>

<style scoped lang="scss">
.loading {
  text-align: center;
  color: white;
}
</style>
