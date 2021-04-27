<template>
  <main class="startQuiz">
    <header>
      <div class="title">
        <h2>Kunst quiz</h2>
      </div>

      <div class="subTitle">
        <p>Quizje doen? Dat kan!</p>
        <p>Daar is deze site voor...</p>
      </div>
    </header>

    <div class="startButton">
      <input type="hidden" v-on:keyup="enterClicked" />
      <button
        data-hover="Let's quiz!"
        @click="switchComponent('quiz')"
        :disabled="currentComp === 'quiz'"
      >
        <div>Klik hier!</div>
      </button>
    </div>
  </main>
</template>

<script>
import { bus } from "./../main.js";

export default {
  name: "startQuiz",

  props: {
    currentComp: {
      type: String,
      required: true,
    },
  },

  data() {
    return {
      t: false,
    };
  },

  created: function () {
    document.addEventListener("keyup", this.enterClicked);
  },
  destroyed: function () {
    document.removeEventListener("keyup", this.enterClicked);
  },

  methods: {
    switchComponent(comp) {
      bus.$emit("switchComp", comp);
    },

    enterClicked(e) {
      console.log(" asdfasdf");
      if (e.keyCode === 13) {
        this.switchComponent("quiz");
      }
    },
  },
};
</script>

<style scoped lang="scss">
@import "./../styles/main.scss";

.startQuiz {
  height: 40%;
  width: 60%;
  margin-left: 20%;
  display: flex;
  justify-content: space-evenly;
  flex-direction: column;
  text-align: center;

  header {
    .title {
      margin-top: -2rem;
      margin-bottom: 1rem;
    }
  }
}

// Button magic
.startButton {
  min-width: 500px;
  margin: 10% auto;
  text-align: center;

  a:hover {
    border-bottom: 1px solid #111;
  }
  h1 {
    font-size: 2em;
    padding: 20px 0;
  }
  p {
    font-size: 0.75em;
    text-transform: uppercase;
    letter-spacing: 2px;
    padding: 20px 0;
  }

  button:hover {
    cursor: pointer;
  }
  button {
    background: transparent;
    outline: none;
    position: relative;
    border: 2px solid #111;
    padding: 15px 50px;
    overflow: hidden;
  }

  button:hover:before {
    opacity: 1;
    transform: translate(0, 0);
  }
  button:before {
    content: attr(data-hover);
    position: absolute;
    top: 1.1em;
    left: 0;
    width: 100%;
    text-transform: uppercase;
    letter-spacing: 3px;
    font-weight: 800;
    font-size: 0.8em;
    opacity: 0;
    transform: translate(-100%, 0);
    transition: all 0.3s ease-in-out;
  }
  button:hover div {
    opacity: 0;
    transform: translate(100%, 0);
  }
  button div {
    text-transform: uppercase;
    letter-spacing: 3px;
    font-weight: 800;
    font-size: 0.8em;
    transition: all 0.3s ease-in-out;
  }
}

.startButton,
.startButton:before,
.startButton:after {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
  text-decoration: none;
  color: #111;
}
</style>



