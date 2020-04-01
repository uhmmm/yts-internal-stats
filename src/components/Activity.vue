<template>
  <div>
    <div class="activity__header">
      <div class="header__single activity__status">Status</div>
      <div class="header__single activity__time">Time</div>
      <div class="header__single activity__by">By</div>
      <div class="header__single activity__activity">Activity</div>
      <div class="header__single activity__details">Details</div>
    </div>

    <ul>
      <li v-for="activity in activities" :key="activity.id" class="activity__entry">
      <div class="entry__single activity__status">{{activity.id}}</div>
      <div class="entry__single activity__time">{{convertTime(activity.timestamp)}}</div>
      <div class="entry__single activity__by">
        <div :class="activity.action_type">
        <!-- {{activity.action_type}} -->
        </div>
      </div>
      <div class="entry__single activity__activity">{{activity.activity}}</div>
      <div class="entry__single activity__details">{{activity.details}}</div>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';
import anime from 'animejs';
import moment from 'moment';

export default {
  name: 'Activity',
  data() {
    return {
      activities: []
    }
  },
  mounted() {
    axios
    .get('https://zummie.com/yt888/items/internal_stats?sort=-timestamp&limit=50')
    .then(response => {
      this.activities = response.data.data;
    })
    .then(() => {
      console.log(moment);
      this.initialAnimation();
    })
  },
  methods: {
    initialAnimation() {
      anime({
        targets: 'li',
        opacity: 1,
        translateY: -2,
        delay: (el, i)=> {
          return i * 20
        },
        duration: 500,
        easing: 'easeInOutSine'
      });

      anime({
        targets: '.entry__single',
        backgroundColor: '#fff1c2',
        delay: (el, i)=> {
          return i * 20
        },
        duration: 500,
        easing: 'easeInOutSine'
      });
    },
    convertTime(time) {
      console.log(time);
      let utcTime = moment.utc(time);
      let localTime = moment(utcTime).local();
      return localTime.fromNow();
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../styles/global';

.activity__header {
  width: 100%;
  display: flex;
  font-family: 'Flaco-mono';
  font-size: .8rem;
  font-weight: 100;
  text-transform: uppercase;
}

.header__single {
  padding: .75rem .8rem;
  border-left: 1px solid $second-color;
  border-bottom: 1px solid $accent;
  color: $third-color;
}

li { opacity: 0; }

.activity__status { width: 5rem; }
.activity__by { width: 3.2rem; }
.activity__time { width:10rem; }
.activity__activity { width: 20%; }
.activity__details { width: calc(100% - 20% - 18.2rem); }

.activity__entry {
  display: flex;
  width: 100%;
  font-family: 'DIN-Regular';
  font-weight: 100;
}

.entry__single {
  padding: 1rem .8rem;
  border-left: 1px dotted $second-color;
  border-bottom: 1px dotted $accent;
  color: $third-color;
  font-size: .9rem;
  line-height: 1.5rem;
  background: $third-color;
}

.bot {
  width: 24px;
  height: 24px;
  background-image: url("../assets/bot.svg");
  background-repeat: no-repeat;
}

.human {
  width: 24px;
  height: 24px;
  background-image: url("../assets/human.svg");
  background-repeat: no-repeat;
}
</style>