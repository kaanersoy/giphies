<template>
  <div class="header">
    <div class="img-box">
      <img :src="logo" alt="Giphies Logo">
    </div>
    <div class="title">
      <img :src="headerText" alt="Popular gifs for everybody">
      <p>powered by GiphyAPI</p>
    </div>
  </div>
</template>

<script>
import logo from '../assets/giphies.svg'
import headerText from '../assets/header-text.svg'
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data: () => {
    return {
      logo,
      headerText
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

#app.dark .header .img-box img{filter: drop-shadow(0 0 24px #fff);}
#app.dark .header .title img{filter: drop-shadow(0 0 10px #fff);}
#app.dark .header .title p{color: rgb(114, 114, 114);}
.header{width: 100%;padding: 50px 0;padding-bottom: 15px;}
.header .img-box{width: 200px;height: auto;display: block; margin: 0 auto;cursor: pointer;}
.header .img-box img{width: 100%;transition: 2s;filter: drop-shadow(5px 5px 10px rgb(187, 187, 187));}
.header .title{width: 400px; margin: 0 auto;padding: 50px 0 10px 0;}
.header .title img{width: 100%;}
.header .title p{padding-top: 10px;font-size: 10px; text-align: center;}
@media screen and (max-width: 1200px) {
  .header .title{width: 320px;}
}
</style>
