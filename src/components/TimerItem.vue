<template>
  <div class="timer-wrapper">
    <div v-bind:class="{ pausedBorder: timer.paused }" class="timer-count">
      <span
        v-if="timer.hours > 0"
        v-bind:class="{ paused: timer.paused }"
        class="hours"
      >
        {{ timer.hours }}:
      </span>
      <span
        v-if="timer.minutes > 0"
        v-bind:class="{ paused: timer.paused }"
        class="minutes"
      >
        {{ timer.minutes }}:
      </span>
      <span v-bind:class="{ paused: timer.paused }" class="seconds">
        {{ timer.seconds }}
      </span>
    </div>
    <div class="timer-controls">
      <span @click="$emit('start', timer.id)" class="play" v-if="timer.paused">
        <svg
          width="17"
          height="20"
          viewBox="0 0 17 20"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            v-bind:class="{ paused: timer.paused }"
            d="M0 20V0L17 10L0 20Z"
            fill="#fff"
          />
        </svg>
      </span>
      <span @click="$emit('pause', timer.id)" class="pause" v-else>
        <svg
          width="10"
          height="20"
          viewBox="0 0 10 20"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <rect
            v-bind:class="{ paused: timer.paused }"
            x="7"
            width="3"
            height="20"
            fill="white"
          />
          <rect
            v-bind:class="{ paused: timer.paused }"
            width="3"
            height="20"
            fill="white"
          />
        </svg>
      </span>
      <span @click="$emit('stop', timer.id)" class="stop">
        <svg
          width="20"
          height="20"
          viewBox="0 0 20 20"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <rect
            v-bind:class="{ paused: timer.paused }"
            width="20"
            height="20"
            fill="white"
          />
        </svg>
      </span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    timer: {
      type: Object
    }
  }
};
</script>

<style scoped>
.paused {
  color: #9e9e9e;
  fill: #9e9e9e;
}

.timer-wrapper {
  height: 120px;
  width: 225px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 10px 10px;
  background: #696969;
}

.timer-count {
  height: 50%;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  border-bottom: 1px solid white;
  font-family: Arial, Helvetica, sans-serif;
  color: #fff;
  font-size: 30px;
}
.pausedBorder {
  border-bottom: 1px solid #9e9e9e;
}
.timer-controls {
  height: 50%;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.timer-controls span {
  margin: 0 20px;
  cursor: pointer;
}
</style>
