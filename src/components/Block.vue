<template>
  <div :class="$style.block" v-if="showBlock" @click="stopTimer">
    Click me!
  </div>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Block',
  props: ['delay'],
  data() {
    return {
      showBlock: false,
      timer: null,
      reactionTime: 0,
    };
  },
  methods: {
    startTimer() {
      this.timer = setInterval(() => {
        this.reactionTime += 10;
      }, 10);
    },
    stopTimer() {
      clearInterval(this.timer);
      this.$emit('end', this.reactionTime);
    },
  },
  mounted() {
    setTimeout(() => {
      this.showBlock = true;
      this.startTimer();
    }, this.delay);
  },
});
</script>

<style module lang="scss">
  .block {
    width: 400px;
    border-radius: 20px;
    background-color: rgb(93, 153, 133);
    color: white;
    text-align: center;
    padding: 100px 0;
    margin: 40px auto;
    font-size: 20px;
    font-weight: 700;
  }
</style>
