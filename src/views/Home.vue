<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
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
