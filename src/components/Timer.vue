<template>
  <div class="timer">
    Timer
    <div>
      <div class="extra-tags__timer">{{stringTimerCounter}}</div>
      <div v-if="timer === 0">
        <div class="btn" @click="startTimer()">Start</div>
      </div>
      <div v-else>
        <div class="btn" @click="stopTimer()">Stop</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Timer',
  data: () => ({
    timer: 0,
    timerCount: 0,
  }),
  computed: {
    stringTimerCounter() {
      let seconds = (this.timerCount % 60).toString().length === 1 ? '0' + (this.timerCount % 60) : (this.timerCount % 60);
      let minutes = (Math.floor(this.timerCount / 60) % 60).toString().length === 1 ? '0' + (Math.floor(this.timerCount / 60) % 60) : (Math.floor(this.timerCount / 60) % 60);
      let hours = (Math.floor(this.timerCount / 60 / 60)).toString().length === 1 ? '0' + (Math.floor(this.timerCount / 60 / 60)) : (Math.floor(this.timerCount / 60 / 60));
      return hours + ':' + minutes + ':' + seconds;
    },
  },
  methods: {
    startTimer() {
      this.timer = setInterval(() => {
        this.timerCount++;
      }, 1000);
    },
    stopTimer() {
      clearTimeout(this.timer);
    },
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

.extra-tags__timer {
  margin-top: 15px;
  font-family: 'HelveticaNeue', sans-serif;
  font-style: normal;
  font-weight: bold;
  font-size: 24px;
  line-height: 30px;
  margin: 0 auto 15px;
  color: inherit;
}
.btn {
  border:1px #42b983 solid;
  padding: 10px;
  border-radius: 5px;
  max-width: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
}
</style>
