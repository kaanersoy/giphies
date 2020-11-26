<template>
  <div id="app" v-bind:class="{ dark: nightMode }">
    <div class="floating-button" v-bind:class="{ dark: nightMode }" >
      <label class="night-switcher" @mousedown="nightSwitcher">
        <input type="checkbox">
        <div class="button">
        </div>  
      </label>
    </div>
    <Header/>
    <Body :gifs="this.gifs"/>
  </div>
</template>

<script>
import axios from 'axios'
import Header from './components/Header'
import Body from './components/Body'
export default {
  name: 'App',
  components: {
    Header,
    Body
  },
  data: () => {
    return {
      gifs: null,
      isLoading: true,
      nightMode: false,
    }
  },
  methods: {
    nightSwitcher: function(){
      this.nightMode ? this.nightMode = false : this.nightMode = true;
    }
  },
  mounted(){
    axios
    .get(`https://api.giphy.com/v1/gifs/trending?api_key=JFd9gYTNz27c8QH4uuS3Aovtn5hp2B1s`)
    .then(res => (this.gifs = res.data.data), this.isLoading=false)
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
}
img{
  display: block;
  vertical-align: center;
}
:root{
  --body-background: white;
  --night-body-background: black;
}
#app{
  background: var(--body-background);
  transition: 200ms background-color;
}
#app.dark{
  background: var(--night-body-background);
}
.floating-button{
  position: absolute;
  top: 10px;
  right: 10px;
}

.night-switcher{
  position: relative;
  width: 50px;
  height: 35px;
  background: black;
  display: flex;
  align-items: center;
  padding: 4px;
  border-radius: 15px;
  cursor: pointer;
}
.night-switcher .button{
  border-radius: 50%;
  width: 30px;
  height: 30px;
  background: white;
  transition: 200ms;
  display: flex;
  align-items: center;
  justify-content: center;
  
}
.night-switcher input{
  position: absolute;
  width: 0;
  height: 0;
}
.night-switcher input:checked ~ .button{
  transform: translateX(20px);
}
.floating-button.dark .night-switcher{
  background: white;
}
.floating-button.dark .night-switcher .button{
  background: black;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
