<template>
  <div :class="$style.content">
    <p>Reaction time: {{ score }} ms</p>
    <h4>{{ rank }}</h4>
  </div>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Results',
  props: ['score'],
  data() {
    return {
      rank: null,
    };
  },
  mounted() {
    if (this.score < 250) {
      this.rank = 'Ninja speed!';
    } else if (this.score < 400) {
      this.rank = 'Rapid reflexes';
    } else {
      this.rank = 'Snail pace...';
    }
  },
});
</script>

<style module lang="scss">
  .content {
    max-width: 300px;
    border-radius: 10px;
    background-color: rgb(191, 236, 221);
    color: rgb(48, 48, 48);
    text-align: center;
    padding: 20px 40px;
    margin: 40px auto;
  }
</style>
