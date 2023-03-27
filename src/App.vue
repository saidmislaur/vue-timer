<template>
  <div id="app">
    <div class="container">
      <div class="timers">
        <Timer v-for="item in timersList" v-bind:key="item" />
        <div @click="addTimer" class="timers__plus">
          <span>+</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Timer from '@/components/Timer.vue';

export default {
  name: 'App',

  data: function () {
    return {
      timersList: [0, 1],
    };
  },
  methods: {
    addTimer() {
      this.timersList.push(this.timersList.length - 1 + 1);
    },
  },
  components: {
    Timer,
  },
};
</script>

<style lang="scss">
.timers {
  padding-top: 70px;
  display: flex;
  justify-content: space-evenly;
  flex-wrap: wrap;

  &__plus {
    width: 220px;
    height: 135px;
    background: #696969;
    text-align: center;
    margin-bottom: 45px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 40px;
    color: #9e9e9e;
    cursor: pointer;
  }
}

* {
  padding: 0;
  margin: 0;
}
#app {
  background: #353638;
  height: 100vh;
}
.container {
  width: 50%;
  margin: 0 auto;
}
</style>
