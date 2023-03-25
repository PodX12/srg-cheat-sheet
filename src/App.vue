<template>
  <HelloWorld v-if="!view" />
  <ComsView v-if="view == 'coms'" />
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import ComsView from './components/ComsView.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    ComsView
  },
  data() {
    return {
      view: ""
    }
  },
  created() {
    let hashSplit = window.location.href.split("#");

    if (hashSplit[1]) {
      let slashSplit = hashSplit[1].split("/").filter(n => n);

      if (slashSplit[0] == "coms") {
        this.view = slashSplit[0];
      }
    }
  }
}
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.obs-main {
  background-color: green;
  width: 1920px;
  height: 1080px;
  background-image: url("./assets/cct-bg.png");
}

body {
  background-color: #333;
  color: #CCCCCC;
  text-shadow: 1px 1px 1px #000000;
  margin: 0;
  font-family: 'Minecraft', sans-serif;
  -webkit-text-stroke-width: 0.5px;
  -webkit-text-stroke-color: #333333;
}
</style>
