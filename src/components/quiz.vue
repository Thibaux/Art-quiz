<template>
  <main>
    <header>
      <h4>Vraag {{ vraagID }}</h4>
    </header>

    <section>
      <div class="question">
        <div class="artPiece">
          <img src="./img.jpg" alt="" />
          <div class="hints"></div>
        </div>
      </div>
      <div class="multipleChoice">
        <div class="choices">
          <div class="choiceOne">
            <button
              v-bind:class="[isActive1 ? 'notClicked' : 'active']"
              @click="isActive1 = !isActive1"
            >
              <div class="choiceText">
                Contrary to popular belief, Lorem Ipsum is not simply random
                text. It ha C
              </div>
            </button>
          </div>
          <div class="choiceTwo">
            <button
              v-bind:class="[isActive2 ? 'notClicked' : 'active']"
              @click="isActive2 = !isActive2"
            >
              <div class="choiceText">Antwoord C</div>
            </button>
          </div>
          <div class="choiceThree">
            <button
              v-bind:class="[isActive3 ? 'notClicked' : 'active']"
              @click="isActive3 = !isActive3"
            >
              <div class="choiceText">Antwoord C</div>
            </button>
          </div>
          <div class="choiceFour">
            <button
              v-bind:class="[isActive4 ? 'notClicked' : 'active']"
              @click="isActive4 = !isActive4"
            >
              <div class="choiceText">Antwoord D</div>
            </button>
          </div>
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
      isActive1: true,
      isActive2: true,
      isActive3: true,
      isActive4: true,
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
// Main
main {
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: 100%;
}

// Header
header {
  position: absolute;
  left: 2em;
  top: 3em;
}

// Content
section {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  height: 80%;
}

// Question
.question {
  width: 100%;

  .artPiece {
    // width: 900px;
    // height: 750px;
    width: 50%;
    height: auto;
    margin-left: 15%;

    img {
      width: 100%;
      height: auto;
    }
  }
}

// Choices
.multipleChoice {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 30%;
  margin-left: -20%;
  margin-right: 2%;

  .choices {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: flex-end;
    flex-wrap: wrap;
    width: 20rem;
    height: 8em;

    // Choice buttons
    button {
      width: auto;
      height: 50px;
      position: relative;
      margin-bottom: 25px;
      border-radius: 32px;
      text-align: center;
      cursor: pointer;
      transition: all 0.1s ease-in-out;
      text-transform: uppercase;
      letter-spacing: 2px;
      overflow: hidden;
      font-weight: 800;
      font-size: 0.6em;
      padding: 0.3em;
      background-color: #dadce0;

      &:hover {
        opacity: 1;
        text-decoration: none;
        color: #ba9ea7;
        background-color: #27375c;
      }
    }

    .active {
      opacity: 0.8;
      color: #79e3b6;
    }
  }

  // Choice
  .choiceText {
    padding-left: 1em;
    padding-right: 1em;
  }
}

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