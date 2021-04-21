<template>
  <div id="app">
    <component :is="currentComp"></component>

    <footer>
      <p class="text">&#169; Thibaux Swildens</p>
      <a href="https://github.com/Thibaux" target="_blank">
        <img src="./assets/content/img/githubIcon.png" alt="githubIcon" />
      </a>
    </footer>
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

  footer {
    position: fixed;
    left: 0;
    bottom: 0;
    width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: center;
    text-align: center;
    align-items: center;
    margin-bottom: 0.2rem;

    .text {
      font-size: 50%;
      margin-right: 0.5rem;
    }

    img {
      width: 20px;
      height: auto;
    }
  }
}
</style>
