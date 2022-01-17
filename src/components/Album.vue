<template>
  <div class="col">
    <img class="album-pic" :src="album.poster" :alt="album.title" />
    <h1 class="fs-4">
      {{ album.title }}
    </h1>
    <h2 class="fs-5">
      {{ album.author }}
    </h2>
    <h3 class="fs-5">
      {{ album.year }}
    </h3>
  </div>
</template>

<script>
export default {
  name: "Album",
  props: ['album']
};
</script>

<style scoped lang="scss">
.col {
  background-color: #2e3a46;
  text-align: center;
  padding: 1em;
  .album-pic {
    width: 100%;
    margin-bottom: 0.5em;
  }
  h1 {
    text-transform: uppercase;
    color: white;
  }
  h2,
  h3 {
    color: grey;
  }
}
</style>
