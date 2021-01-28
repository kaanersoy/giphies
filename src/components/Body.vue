<template>
  <div class="container">
      <ul class="gifs">
        <li v-for="gif in gifs" :key="gif.id" @click="isItemClicked">
            <img :src="ghostImage" :id="'ghost-' + gif.id" v-bind:class="{ invisible : loadedGifs.includes(gif.id) }" >
            <img :src="gif.images.fixed_width_small.url" @load="pushLoadedGif" :alt="gif.id" :id="gif.id">
        </li>
      </ul>
      <!-- <ClickedImage v-if="clickedActive" :source="ghostImage" :name="'clickedItemName'" :url="'ghostImage'" @clicked="onClickChild"/> -->
      <ClickedImage v-if="clickedActive" :source="clickedItemUrl" :name="clickedItemName" :url="clickedItemUrl" :download="clickedItemDownloadUrl"  @clicked="onClickChild"/>
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
        clickedItemDownloadUrl: null
      }
    },
    methods: {
      pushLoadedGif: function(e){
        this.loadedGifs.push(e.target.id);
      },
      isItemClicked: async function(e){
        this.clickedItemId = e.target.id;
        const selectedGif = this.gifs.filter(gif => gif.id == this.clickedItemId)[0];
        this.clickedActive = true;
        this.clickedItemUrl = selectedGif.images.fixed_height.url;
        this.clickedItemName = selectedGif.title;
        this.clickedItemDownloadUrl = selectedGif.images.fixed_width.url;
      },
      onClickChild (isActive) {
        this.clickedActive = isActive;
      }
    }
}
</script>

<style>
.container{max-width: 1400px; width: 80%;margin: 0 auto;padding-bottom: 100px;}
.gifs{ column-count: 4; display: block;}
.gifs li{list-style: none; margin-bottom: 30px;border-radius: 5px;overflow: hidden;}
.gifs li img{width: 100%;}
@media screen and (max-width: 1200px) {
  .gifs{column-count: 2;}
}
.gifs img.invisible{display: none;}

</style>