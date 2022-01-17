<template>
  <main class="container pb-4">
    <div 
    class="row row-cols-6 gap-3"
    v-if="albums">
      <Album 
      v-for="(album, index) in albums" 
      :key="index"
      :album="album"
      />
    </div>
    <div 
    class="row loading"
    v-else>
        <div class="col-12">
            <h1>Loading...</h1>
        </div>
    </div>
  </main>
</template>

<script>
import axios from "axios";
import Album from './Album.vue'

export default {
  name: "Main",
  components: {
      Album,
  },
  data() {
    return {
      albums: null,
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
              })
              .catch((error) => {
                console.log(error);
              });  
        }, 1000);
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
