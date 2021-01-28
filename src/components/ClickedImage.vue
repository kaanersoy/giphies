<template>
  <div class="clicked-wrapper">
      <div class="clicked-item">
          <div class="clicked-content">
              <p>{{ name }}</p>
              <img :src="source" :alt="name" @load="isClickedLoaded = true" v-show="isClickedLoaded">
              <img :src="ghostImage" v-show="!isClickedLoaded">
              <div class="button-wrapper">
                <a :href="url" target="_blank">Visit in GIPHY |<img :src="DownloadIcon" alt=""></a>
              </div>
          </div>
          <button @click="closeTab">x</button>
      </div>
  </div>
</template>

<script>
import DownloadIcon from '../../static/download-icon.svg';
import ghostImage from '../../static/image-loading.gif';
export default {
    name: 'ClickedImage',
    data: () =>{
        return {
            DownloadIcon,
            ghostImage,
            isClickedLoaded: false
        }
    },
    props:{
        source: {
            type: String,
            required: true
        },
        url: {
            type: String,
            required: true
        },
        name: {
            type: String,
            required: true
        },
        download: {
            type: String,
            required: true
        }
    },
    methods:{
        closeTab: function (isActive) {
            isActive = false;
            this.$emit('clicked', isActive);
        },
    }
}
</script>

<style>
    .clicked-wrapper{
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100vh;
        background: rgba(255,255,255,0.5);
        filter: blur(0.3);
    }
    .clicked-wrapper .clicked-item{
        width: 35%;
        margin: 0 auto;
        position: relative;
        margin-top: 30px;
        border-radius: 50px;
    }
    .clicked-wrapper .clicked-item img{
        min-width: 100%;
        max-height: 80vh;
    }
    .clicked-wrapper .clicked-item .button-wrapper{}
    .clicked-wrapper .clicked-item .button-wrapper a{display: flex;}
    .clicked-wrapper .clicked-item .button-wrapper a img{display: inline-block; width: 1em;margin-left: 10px; height: 1em;min-width: unset;max-height: unset;display: inline;}
    .clicked-wrapper .clicked-item button{
        position: absolute;
        top: -7px;
        right: -15px;
        width: 50px;
        height: 50px;
        border-radius: 50%;
        border: none;
        background-color: #fef0ae;
        filter: drop-shadow(0px 0px 0.25rem  rgba(0, 0, 0, 0.274));
        font-size: 15px;
    }
    .clicked-wrapper .clicked-item .clicked-content{}
    .clicked-wrapper .clicked-item .clicked-content p{text-align: center; width: 80%;margin: 0 auto;display: block;width: 100%;background-color: #fef0ae;padding: 10px 0;font-size: 14px;}
    .clicked-wrapper .clicked-item .clicked-content a{background: #fef0ae;display: block; width: 100%; text-align: center;color: #000;padding: 20px;font-size: 15px;}

    @media screen and (max-width: 414px) {
        .clicked-wrapper .clicked-item{
            width: 80%;
        }
        .clicked-wrapper .clicked-item img{
            width: 100%;
            max-height: 80vh;
        }
        .clicked-wrapper .clicked-item .clicked-content p{
            padding: 10px 50px;
        }
    }
</style>