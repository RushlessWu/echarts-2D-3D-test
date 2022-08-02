<template>
  <div id="app">
    <button @click="changeViewPoint = !changeViewPoint">切换</button>
    <map3D v-if="changeViewPoint" />
    <map2D v-else />
  </div>
</template>

<script>
import map2D from "./components/map2D.vue";
import map3D from "./components/map3D.vue";

export default {
  name: "App",
  components: {
    map2D,
    map3D,
  },
  data() {
    return {
      changeViewPoint: true,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
