<template>
  <div class="home">
    <Timer />
    <Puzzle />
  </div>
</template>


<script>
// @ is an alias to /src
import Timer from '@/components/Timer.vue'
import Puzzle from '@/components/Puzzle.vue'

export default {
  name: 'Home',
  components: {
    Timer,
    Puzzle
  }
}
</script>

<style>
body {
  background: linear-gradient(169.68deg,#3f298d 6.91%,#1a0657 20.42%,#1d1b29 38.25%);
  color: #fff;
}
section {
  display: flex;
  width: auto;
  justify-content: center;
}
</style>