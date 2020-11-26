<template>
  <div class="container">
      <ul class="gifs">
        <li v-for="gif in gifs" :key="gif.id">
            <img :src="gif.images.fixed_height.url" alt="">
        </li>
      </ul>
  </div>
</template>

<script>
export default {
    name: "Body",
    props: {
      gifs: null
    },
    components: {
    },
    data: () => {
      return{

      }
    }
}
</script>

<style>
.container{max-width: 1400px; width: 80%;margin: 0 auto;padding-bottom: 100px;}
.gifs{ column-count: 4; display: block;}
.gifs li{list-style: none; margin-bottom: 30px;}
.gifs li img{width: 100%;}
@media screen and (max-width: 1200px) {
  .gifs{column-count: 2;}
}

</style>