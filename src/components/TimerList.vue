<template>
  <div class="wrapper">
    <TimerItem
      v-for="timer in timers"
      :key="timer.id"
      :timer="timer"
      @start="start"
      @pause="pause"
      @stop="stop"
    />
    <button @click="$emit('add-timer')" class="add-timer">+</button>
  </div>
</template>

<script>
import TimerItem from "@/components/TimerItem";
export default {
  props: ["timers"],
  components: {
    TimerItem
  },
  methods: {
    start(id) {
      this.$emit("start", id);
    },
    pause(id) {
      this.$emit("pause", id);
    },
    stop(id) {
      this.$emit("stop", id);
    }
  }
};
</script>

<style scoped>
.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
}

.add-timer {
  height: 120px;
  width: 225px;
  margin: 10px 10px;
  border: none;
  background: #696969;
  font-size: 50px;
  color: #fff;
  cursor: pointer;
}
</style>
