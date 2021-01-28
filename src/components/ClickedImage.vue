<template>
  <div class="clicked-wrapper">
      <div class="clicked-item">
          <img :src="source" :alt="name">
          <div class="clicked-content">
              <p>{{ name }}</p>
              <a :href="url" target="_blank">go to image</a>
          </div>
      </div>
  </div>
</template>

<script>
export default {
    name: 'ClickedImage',
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
        }
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
        background: #fff;
    }
    .clicked-wrapper .clicked-item{}
    .clicked-wrapper .clicked-item img{}
</style>