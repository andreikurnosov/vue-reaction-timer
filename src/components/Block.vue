<template>
  <div class="block" v-if="showBlock" @click="stopTimer">
    Click me
  </div>
</template>

<script>
import { ref } from 'vue'
export default {
  props: {
    delay: {
      required: true
    }
  },
  setup(props, { emit }) {
    const showBlock = ref(false)
    const timer = ref(null)
    const reactionTime = ref(0)

    function startTimer() {
      timer.value = setInterval(() => {
        reactionTime.value += 10
      }, 10)
    }

    function stopTimer() {
      emit('end', reactionTime.value)
      clearInterval(timer)
    }

    setTimeout(() => {
      showBlock.value = true
      startTimer()
    }, props.delay)

    return {
      showBlock,
      stopTimer
    }
  }
}
</script>

<style>
.block {
  width: 400px;
  border-radius: 20px;
  background: rgb(34, 193, 195);
  background: linear-gradient(
    90deg,
    rgba(34, 193, 195, 1) 0%,
    rgba(253, 187, 45, 1) 100%
  );
  color: white;
  text-transform: uppercase;
  font-weight: bold;
  text-shadow: grey 4px 2px 2px;
  font-size: 5rem;
  text-align: center;
  padding: 100px 20px;
  margin: 40px auto;
  transition: all 200ms;
}
</style>
