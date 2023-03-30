<template>
  <div class="timer">
    <div class="timer__head">
      <span :class="{ active: isStart }">{{ timer }}</span>
    </div>
    <div class="timer__footer">
      <StopIcon v-if="isStart === true" @click="pauseTimer" />
      <PlayIcon v-else @click="playTimer" />
      <ClearIcon :active="isStart" @click="stopTimer" />
    </div>
  </div>
</template>

<script>
import PlayIcon from '@/components/icons/play.vue';
import StopIcon from '@/components/icons/stop.vue';
import ClearIcon from '@/components/icons/clear.vue';
export default {
  data() {
    return {
      seconds: 0,
      timerId: null,
      isStart: false,
    };
  },
  computed: {
    timer() {
      const totalMinutes = Math.floor(this.seconds / 60);
      const seconds = this.seconds % 60;
      const hours = Math.floor(totalMinutes / 60);
      const minutes = totalMinutes % 60;

      const hoursDisplay = hours === 0 ? '' : `${hours}:`;
      const minutesDisplay = minutes === 0 ? '' : `${minutes}:`;

      return `${hoursDisplay}${minutesDisplay}${seconds}`;
    },
  },
  methods: {
    playTimer() {
      this.timerId = setInterval(() => {
        this.seconds++;
      }, 1000);
      this.isStart = true;
    },
    stopTimer() {
      if (this.timerId) {
        clearInterval(this.timerId);
        this.seconds = 0;
        this.isStart = false;
      }
    },
    pauseTimer() {
      if (this.timerId) {
        clearInterval(this.timerId);
        this.isStart = false;
      }
    },
  },
  components: {
    PlayIcon,
    StopIcon,
    ClearIcon,
  },
};
</script>

<style lang="scss" scoped>
.timer {
  width: 220px;
  background: #696969;
  text-align: center;
  margin-bottom: 45px;

  &__head {
    padding: 22px;
    border-bottom: 1px solid #9e9e9e;

    span {
      font-family: 'Gotham Pro';
      font-weight: 400;
      font-size: 22px;
      line-height: 21px;
      color: #9e9e9e;

      &.active {
        color: white;
      }
    }
  }
  &__footer {
    padding: 22px;
    display: flex;
    justify-content: space-evenly;

    svg {
      cursor: pointer;

      &.active {
        fill: '#FFFF';
      }
    }
  }
}
</style>
