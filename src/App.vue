<template>
  <div id="app">
    <CEP />
  </div>
</template>

<script>
import Vue from "vue";
import VueMask from "v-mask";
Vue.use(VueMask);
import CEP from "./components/CEP.vue";
export default {
  name: "App",
  components: {
    CEP
  }
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background: linear-gradient(
    to bottom,
    rgba(230, 230, 230, 0.7),
    rgba(230, 230, 230, 0.7)
  );
}
#app {
  font-family: Trebuchet MS;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #006eff;
}
</style>
