<template>
  <div class="wrap-app">
    <main-screen
      v-if="statusMatch === 'default'"
      @onStart="onHandleBeforeStart($event)"
    ></main-screen>
    <InteractScreen
      v-if="statusMatch === 'match'"
      :cardsContext="settings.cardsContext"
      @onFinish="onGetResult($event)"
      @onStartAgain="statusMatch = 'default'"
    ></InteractScreen>
    <ResultScreenVue
      :timer="timer"
      v-if="statusMatch === 'results'"
      @onStartAgain="statusMatch = 'default'"
    ></ResultScreenVue>
  </div>
</template>
<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import ResultScreenVue from "./components/ResultScreen.vue";
import { shuffled } from "./utils/array";

export default {
  name: "App",
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        cardsContext: [],
        startedAt: null,
        timer: null,
      },
      statusMatch: "default",
    };
  },
  components: {
    MainScreen,
    InteractScreen,
    ResultScreenVue,
  },
  methods: {
    onHandleBeforeStart(config) {
      this.settings.totalOfBlocks = config.totalOfBlocks;
      const firstCards = Array.from(
        { length: this.settings.totalOfBlocks / 2 },
        (_, i) => i + 1
      );
      const secondCard = [...firstCards];
      const card = [...firstCards, ...secondCard];
      this.settings.cardsContext = shuffled(shuffled(shuffled(card)));
      this.settings.startedAt = new Date().getTime();
      this.statusMatch = "match";
    },
    onGetResult() {
      // Get timer
      this.timer = new Date().getTime() - this.settings.startedAt;
      // switch to results components
      this.statusMatch = "results";
    },
  },
};
</script>
