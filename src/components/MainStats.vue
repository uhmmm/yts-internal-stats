<template>
  <div class="mainstat">
    <div class="singlestats">
      <h2>Total views</h2>
      <span class="singlestats__numbers">{{ total_views }}</span>
    </div>
    <div class="singlestats">
      <h2>Total videos</h2>
      <span class="singlestats__numbers">{{ total_videos }}</span>
    </div>
    <div class="singlestats">
      <h2>Total subscribers</h2>
      <span class="singlestats__numbers">{{ total_subscribers }}</span>
    </div>
    <div class="singlestats">
      <h2>Total channels</h2>
      <span class="singlestats__numbers">{{ total_channels }}</span>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import anime from 'animejs';

export default {
  name: 'MainStats',
  data (){
    return {
      total_views: 0,
      total_subscribers: 0,
      total_videos: 0,
      total_channels: 0
    }
  },
  mounted () {
    axios
    .get('https://ytchannelcallwebhook.firebaseio.com/stats.json')
    .then(response => {
      response = response.data;
      this.total_views = response.total_views.toString().replace(/\B(?=(\d{3})+(?!\d))/g, "."),
      this.total_subscribers = response.total_subscribers.toString().replace(/\B(?=(\d{3})+(?!\d))/g, "."),
      this.total_videos = response.total_videos.toString().replace(/\B(?=(\d{3})+(?!\d))/g, "."),
      this.total_channels = response.total_channels.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".")
    })
    .then(() => {
        this.initialAnimation();
      }
    )
  },
  methods: {
    initialAnimation() {
      anime({
        targets: 'h2',
        opacity: 1,
        translateY: -2,
        easing: 'easeInOutSine'
      });

      anime({
        targets: '.singlestats__numbers',
        opacity: 1,
        translateY: -2,
        delay: 250,
        duration: 1000,
        easing: 'easeInOutSine'
      });
    }
  }

}
</script>

<style lang="scss" scoped>
@import '../styles/global';

h2 {
  opacity: 0;
}

.mainstat {
  width: 100%;
  display: flex;
}

.singlestats {
  padding: 0 .25rem;
  width: 20%;
}

.singlestats__numbers {
  font-family: 'DIN-Regular';
  margin-top: .5rem;
  font-size: 1.5rem;
  color: $third-color;
  display: block;
  opacity: 0;
}
</style>