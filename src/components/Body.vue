<template>
  <div class="container">
      <div class="search-container">
        <label for="search-input">Search something🙉👇</label>
        <div class="search-group">
          <input type="text"  v-model="search" id="search-input" placeholder="Example search: Dogs" @keyup="searchSomeGifs">
        </div>

      </div>
      <ul v-show="!search" class="gifs">
        <li v-for="gif in gifs" :key="gif.id" @click="isItemClicked">
            <img :src="ghostImage" :id="'ghost-' + gif.id" v-bind:class="{ invisible : loadedGifs.includes(gif.id) }" >
            <img :src="gif.images.fixed_width_small.url" @load="pushLoadedGif" :alt="gif.id" :id="gif.id">
        </li>
      </ul>
      <ul v-if="search" class="gifs">
        <li v-for="gif in searchGifs" :key="gif.id" @click="isItemClicked">
            <img :src="ghostImage" :id="'ghost-' + gif.id" v-bind:class="{ invisible : loadedGifs.includes(gif.id) }" >
            <img :src="gif.images.fixed_width_small.url" @load="pushLoadedGif" :alt="gif.id" :id="gif.id">
        </li>
      </ul>
      <!-- <ClickedImage v-if="clickedActive" :source="ghostImage" :name="'clickedItemName'" :url="'ghostImage'" @clicked="onClickChild"/> -->
      <ClickedImage v-if="clickedActive" :source="clickedItemUrl" :name="clickedItemName" :url="clickedItemUrl" :download="clickedItemDownloadUrl"  @clicked="onClickChild"/>
  </div>
</template>

<script>
import axios from 'axios';
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
        clickedItemDownloadUrl: null,
        search: null,
        searchGifs: [],
        isSearching: false
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
      },
      searchSomeGifs: async function(){
        const apiKey = process.env.VUE_APP_API_KEY;
        axios
        .get(`https://api.giphy.com/v1/gifs/search?api_key=${apiKey}&q=${this.search}&limit=10`)
        .then(res => (this.searchGifs = res.data.data))
      }
    }
}
</script>

<style>
.container{max-width: 1400px; width: 80%;margin: 0 auto;padding-bottom: 100px;}
.container .search-container{padding: 20px 0;width: 60%;margin: 0 auto;position: relative;margin-top: 10px;padding-top: 30px;}
.container .search-container::before{content: ''; position: absolute; top: 0; height: 2px; width: 100%; background: rgba(0, 0, 0, 0.287);left: 0;}
#app.dark .container .search-container::before {background: rgba(255, 255, 255, 0.356);}
.container .search-container label{ margin-bottom: 15px; display: block;font-size: 18px;text-align: center;}
#app.dark .container .search-container label{ color: #fff;}
.container .search-container input{padding: 10px 15px; font-size: 18px;display: block;width: 100%;border: none; background-color: rgba(0, 0, 0, 0.233); border-bottom: 3px solid rgb(100, 100, 100); color: #000;}
#app.dark .container .search-container input{color: #fff; background-color: rgba(255, 255, 255, 0.253); border-bottom: 3px solid rgb(170, 170, 170);}
.gifs{ column-count: 4; display: block;}
.gifs li{list-style: none; margin-bottom: 30px;border-radius: 5px;overflow: hidden;}
.gifs li img{width: 100%;}
@media screen and (max-width: 420px) {
  .gifs{column-count: 2;}
  .container .search-container{width: 100%;}
}
.gifs img.invisible{display: none;}

</style>