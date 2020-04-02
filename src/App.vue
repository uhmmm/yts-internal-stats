<template>
  <div id="app">
    <Loader v-if="loading" />

    <div>
      <div class="bg"></div>
      <h1>Internal stats/bot monitor</h1>
      <MainStats @rmLoader="rmLoader" />

      <h1>Latest bot & human editors activities</h1>
      <Activity @rmLoader="rmLoader" />
    </div>
  </div>
</template>

<script>
import Loader from "./components/Loader.vue";
import MainStats from "./components/MainStats.vue";
import Activity from "./components/Activity.vue";

export default {
  name: "App",
  components: {
    Loader, MainStats, Activity
  },
  data() {
    return {
      loading: true
    }
  },
  mounted() {
    setTimeout(() => this.loading = false, 2000)
  },
  methods: {
    rmLoader() {
      this.loading = false;
    } 
  }
};
</script>

<style lang="scss">
@import 'styles/global';
@import 'styles/reset';

// HEX: #2D68F1
// HEX: #3B3150

@font-face {
  font-family: 'Feijoa-Medium';
  src: url('./assets/fonts/fe-temp.woff') format('woff'); /* Pretty Modern Browsers */
}

@font-face {
  font-family: 'Flaco-Mono';
  src: url('./assets/fonts/fl-mono.woff') format('woff'); /* Pretty Modern Browsers */
}

@font-face {
  font-family: 'DIN-Regular';
  src: url('./assets/fonts/DINNextLTPro-Regular.woff') format('woff'); /* Pretty Modern Browsers */
}

@font-face {
  font-family: 'DIN-Medium';
  src: url('./assets/fonts/DINNextLTPro-Medium.woff') format('woff'); /* Pretty Modern Browsers */
}

* {
  box-sizing: border-box;
}

html {
  font-size: 16px;
}

body {
  background: $base-color;
  margin: 6rem;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

h1 {
  font-family: 'DIN-Medium';
  font-size: 1rem;
  font-weight: 100;
  color: $second-color;
  margin-top: 2rem;
  padding: 1rem .25rem;
  border-bottom: 1px solid $accent;
}

h2 {
  font-family: 'Flaco-Mono';
  font-size: .8rem;
  color: $second-color;
  text-transform: uppercase;
  font-weight: 100;
  margin-top: 1.5rem;
}

.bg {
  width: 100vw;
  height: 100vh;
  background-color: #fff1c2;
  position: fixed;
  z-index: -1000;
  animation: fade-in 1s forwards;
}

@keyframes fade-in {
  0%   { opacity: 0; }
  100% { opacity: 1; }
}
</style>
