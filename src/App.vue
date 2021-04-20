<template>
  <div id="app">
    <startQuiz :current-comp="currentComp"></startQuiz>

    <!-- <component :is="currentComp"></component> -->
  </div>
</template>

<script>
import { bus } from "./main.js";
import StartQuiz from "./components/startQuiz.vue";
import Quiz from "./components/quiz.vue";
import EndQuiz from "./components/endQuiz.vue";

export default {
  name: "App",
  components: {
    StartQuiz,
    Quiz,
    EndQuiz,
  },

  data() {
    return {
      currentComp: "StartQuiz",
    };
  },

  created() {
    bus.$on("switchComp", (comp) => {
      this.currentComp = comp;
    });
  },
};
</script>

<style lang="scss">
@import "./styles/main.scss";

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
  width: 100vw;
  height: 100vh;
}
</style>
