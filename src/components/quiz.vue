<template>
  <main>
    <header>
      <h3>Vraag {{ vraagID }}</h3>
    </header>

    <section>
      <div class="question">
        <div class="artPiece">
          <img src="" alt="" />
          <div class="hints"></div>
        </div>
      </div>
      <div class="multipleChoice">
        <div class="choices">
          <div class="choiceOne"></div>
          <div class="choiceTwo"></div>
          <div class="choiceThree"></div>
          <div class="choiceFour"></div>
        </div>
      </div>
    </section>

    <div class="nextQuestionButton">
      <button>
        <div>Volgende vraag!</div>
      </button>
    </div>

    <div v-if="endQuiz" class="endButton">
      <button
        data-hover="Let's not quiz!"
        @click="switchComponent('endQuiz')"
        :disabled="currentComp === 'endQuiz'"
      >
        <div>Klik hier!</div>
      </button>
    </div>
  </main>
</template>

<script>
import { bus } from "./../main.js";

export default {
  name: "quiz",
  props: {
    currentComp: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      endQuiz: false,
      vraagID: 1,
    };
  },

  methods: {
    switchComponent(comp) {
      bus.$emit("switchComp", comp);
    },

    endQuiz() {
      this.endQuiz === true;
    },
  },
};
</script>

<style scoped lang="scss">
// Next question button
.nextQuestionButton {
  margin: 10% auto;
  text-align: center;

  a:hover {
    border-bottom: 1px solid #111;
  }
  p {
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
    // min-width: 10px;
    // width: 100px;
  }

  button:hover {
    background-color: #27375c;
  }
  button:before {
    position: absolute;
    top: 1.1em;
    left: 0;
    width: 100%;
    text-transform: uppercase;
    letter-spacing: 3px;
    font-weight: 800;
    font-size: 0.8em;
  }
  button:hover div {
    color: #ba9ea7;
  }
  button div {
    text-transform: uppercase;
    letter-spacing: 3px;
    font-weight: 800;
    font-size: 110%;
  }
}

.nextQuestionButton,
.nextQuestionButton:before,
.nextQuestionButton:after {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
  text-decoration: none;
  color: #111;
}

// End quiz button magic
.endButton {
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

.endButton,
.endButton:before,
.endButton:after {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
  text-decoration: none;
  color: #111;
}
</style>