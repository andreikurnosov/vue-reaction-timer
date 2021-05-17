<template>
  <p class="result">Reaction time: {{ score }} ms</p>
  <p class="rank">{{ rank }}</p>
</template>

<script>
import { ref } from 'vue'
export default {
  props: {
    score: {
      required: false
    }
  },
  setup(props) {
    const rank = ref(null)

    if (props.score < 250) {
      rank.value = 'Ninja Fingers'
    } else if (props.score < 400) {
      rank.value = 'Rapid Reflexes'
    } else {
      rank.value = 'Snail pace...'
    }

    return { rank }
  }
}
</script>

<style>
.result {
  font-size: 2rem;
  font-weight: bold;
  color: white;
  padding: 10px;
  border-radius: 10px;
  display: block;
  background: rgb(63, 94, 251);
  background: radial-gradient(
    circle,
    rgba(63, 94, 251, 1) 0%,
    rgba(252, 70, 107, 1) 100%
  );
}

.rank {
  color: rgba(252, 70, 107, 1);
  font-weight: bold;
  font-size: 4rem;
}
</style>
