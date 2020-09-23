<template>
  <div id="app">
    <TimerList
      v-bind:timers="timers"
      @start="start"
      @pause="pause"
      @stop="stop"
      @add-timer="addTimer"
    />
  </div>
</template>

<script>
import TimerList from "@/components/TimerList";

function randomInt(min, max) {
  return Math.random() * (max - min) + min;
}

export default {
  name: "app",
  components: {
    TimerList
  },
  data() {
    return {
      timers: [
        {
          id: 1,
          paused: true,
          ticker: undefined,
          hours: 0,
          minutes: 0,
          seconds: 0,
          timer: 0
        }
      ]
    };
  },
  methods: {
    start(id) {
      let currentTimer = this.timers.find(item => item.id == id);
      currentTimer.ticker = setInterval(() => {
        let minutes = Math.floor(++currentTimer.timer / 60);
        currentTimer.seconds = currentTimer.timer - minutes * 60;
        currentTimer.hours = Math.floor(minutes / 60);
        currentTimer.minutes = minutes - currentTimer.hours * 60;
      }, 1000);
      currentTimer.paused = false;
    },
    pause(id) {
      let currentTimer = this.timers.find(item => item.id == id);
      window.clearInterval(currentTimer.ticker);
      currentTimer.paused = true;
    },
    stop(id) {
      let currentTimer = this.timers.find(item => item.id == id);
      window.clearInterval(currentTimer.ticker);
      currentTimer.timer = 0;
      currentTimer.paused = true;
      currentTimer.seconds = 0;
      currentTimer.minutes = 0;
      currentTimer.hours = 0;
    },
    addTimer() {
      let newTimer = {
        id: randomInt(1, 10000),
        paused: true,
        ticker: undefined,
        hours: 0,
        minutes: 0,
        seconds: 0,
        timer: 0
      };
      this.timers.push(newTimer);
    }
  }
};
</script>

<style>
body {
  background: #353638;
}
</style>
