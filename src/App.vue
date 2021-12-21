<template>
  <h1>Reaction Timer</h1>
  <button class="button" :disabled="isPlaying" @click="start">Play</button>
  <Block v-if="isPlaying" :delay="delay" @end="endGame" />
  <Results :score="score" v-if="showResults" />
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Block from './components/Block.vue';
import Results from './components/Results.vue';

declare interface AppType {
  isPlaying: boolean;
  delay: null | number;
  score: null | number;
  showResults: boolean;
}

export default defineComponent({
  name: 'App',
  components: { Block, Results },
  data(): AppType {
    return {
      isPlaying: false,
      delay: null,
      score: null,
      showResults: false,
    };
  },
  methods: {
    start() {
      this.delay = 2000 + Math.random() * 5000;
      this.isPlaying = true;
      this.showResults = false;
    },
    endGame(reactionTime: number) {
      this.score = reactionTime;
      this.isPlaying = false;
      this.showResults = true;
    },
  },
});
</script>

<style lang="scss">
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  .button {
    border-radius: 10px;
    background-color: rgb(93, 153, 133);
    color: white;
    text-align: center;
    padding: 16px 32px;
    border: none;
    font-size: 16px;
    transition: background-color 0.2s;
    cursor: pointer;

    &:hover {
      background-color: rgb(69, 112, 98);
    }
    &:disabled {
      background-color: rgb(209, 209, 209);
      color: rgb(136, 136, 136);
      cursor: default;
    }
  }
</style>
