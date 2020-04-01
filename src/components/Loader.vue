<template>
  <div class="container">
    <div ref="container" class="animation"></div>
  </div>
</template>

<script>
import lottie from 'lottie-web';
import animationData from '../assets/data.json';

export default {
  name: 'loader',
  mounted() {
    lottie.loadAnimation({
      container: this.$refs.container,
      renderer: 'svg',
      loop: true,
      autoplay: true,
      animationData: animationData
    })
  }

}
</script>

<style lang="scss" scoped>
@import '../styles/global';

.container {
  position: absolute;
  width: 100vw;
  height: 100vh;
  background: $base-color;
  display: flex;
  align-items: center; 
  justify-content: center;
  text-align: center;
  margin-left: -6rem;
  margin-top: -6rem;
  z-index: 100;
}
 .animation {
   width: 200px;
 }

</style>