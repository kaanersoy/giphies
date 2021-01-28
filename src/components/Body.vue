<template>
  <div class="container">
      <ul class="gifs">
        <li v-for="gif in gifs" :key="gif.id" @click="isItemClicked">
            <img :src="ghostImage" :id="'ghost-' + gif.id" v-bind:class="{ invisible : loadedGifs.includes(gif.id) }" >
            <img :src="gif.images.fixed_height.url" @load="pushLoadedGif" :alt="gif.id" :id="gif.id">
        </li>
      </ul>
      <ClickedImage v-if="clickedActive" :source="ghostImage" :name="'sample'" :url="'https://vuejs.org/v2/guide/components-props.html'" />
  </div>
</template>

<script>
import ghostImage from '../../static/image-loading.gif';
import ClickedImage from './ClickedImage.vue';

export default {
    name: "Body",
    props: {
      gifs: null
    },
    components: {
      ClickedImage
    },
    data: () => {
      return{
        loadedGifs: [],
        ghostImage,
        clickedActive: false,
        clickedItemId: null,
        clickedItemUrl: null,
        clickedItemName: null,
      }
    },
    methods: {
      pushLoadedGif: function(e){
        this.loadedGifs.push(e.target.id);
      },
      isItemClicked: async function(e){
        const apiKey = process.env.VUE_APP_API_KEY;
        this.clickedItemId = e.target.id;
        const response = await fetch(`https://api.giphy.com/v1/gifs/${this.clickedItemId}?api_key=${apiKey}`);
        if(response.data){
          console.log(response);
        }else{
          console.log("something wrong😥");
        }
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
.gifs img.invisible{display: none;}

</style>