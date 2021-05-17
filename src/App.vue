<template>
  <h1>
    Reaction Timer ⌚
  </h1>
  <result v-if="showResults" :score="score" />

  <button @click="start" class="btn-play" :disabled="isPlaying">▶</button>
  
  <block v-if="isPlaying" :delay="delay" @end="endGame" />

</template>

<script>
import { ref } from 'vue'
import Block from './components/Block.vue'
import Result from './components/Result.vue'

export default {
  name: 'App',
  components: {
    Block,
    Result
  },

  setup() {
    const isPlaying = ref(false)
    const delay = ref(null)
    const score = ref(null)
    const showResults = ref(false)

    const start = () => {
      showResults.value = false
      isPlaying.value = true
      delay.value = 2000 + Math.random() * 5000
    }

    const endGame = reactionTime => {
      showResults.value = true
      score.value = reactionTime
      isPlaying.value = false
    }

    return {
      start,
      delay,
      isPlaying,
      score,
      endGame,
      showResults
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
}

h1 {
  font-size: 4rem;
  margin-top: 0;
}

.btn-play {
  border: 0;
  border-radius: 5px;
  padding: 10px 30px;
  font-size: 2rem;
  font-weight: bold;
  color: white;
  background: rgb(131, 58, 180);
  background: linear-gradient(
    90deg,
    rgba(131, 58, 180, 1) 0%,
    rgba(253, 29, 29, 1) 50%,
    rgba(252, 176, 69, 1) 100%
  );

  transition: all 300ms linear;
}

.btn-play:hover {
  color: rgb(37, 37, 37);
}

.btn-play:disabled {
  background: grey;
  color: rgb(37, 37, 37);
  cursor: not-allowed;
}
</style>
