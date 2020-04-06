<template>
  <div>
    <b-jumbotron>
      <h3 class="kategori">{{ selectedOption }}</h3>
      <h5>{{ decoder(currentQuestion.question) }}</h5>

      <hr class="my-4">
      <b-list-group>
        <b-list-group-item
          v-for="(answer, index) in shuffledAnswers"
          :key="index"
          @click="selectAnswer(index)"
          :class="answerClass(index)"
        >{{ decoder(answer) }}</b-list-group-item>
      </b-list-group>

      <b-button
        variant="primary"
        @click="submitAnswer"
        :disabled="selectedIndex === null || answered"
        v-if="countModalQuestion < 10"
      >Submit</b-button>

      <b-button
        variant="success"
        @click="next"
        :disabled="answered == false"
        v-if="countModalQuestion < 10"
      >Next</b-button>

      <b-button variant="info" v-b-modal.modal-1 v-else>Finish</b-button>

      <b-modal id="modal-1" title="Result" ok-only @ok="resetQuestions">
        <p class="my-4">
          <b-icon icon="check-circle" variant="success" class="mr-1"></b-icon>
          Correct: {{ countCorrect }}
        </p>
        <p class="my-4">
          <b-icon icon="x-circle" variant="danger" class="mr-1"></b-icon>
          Incorrect: {{ countModalQuestion - countCorrect }}
        </p>
        <p class="my-4">
          <b-icon icon="question-circle-fill" variant="info" class="mr-1"></b-icon>
          Questions: {{ countModalQuestion }}
        </p>
      </b-modal>
    </b-jumbotron>
  </div>
</template>

<script>
import _ from "lodash";

export default {
  props: {
    currentQuestion: Object,
    next: Function,
    increment: Function,
    resetQuestion: Function,
    selectedOption: String
  },
  data() {
    return {
      selectedIndex: null,
      correctIndex: null,
      shuffledAnswers: [],
      answered: false,
      countModalQuestion: 0,
      countCorrect: 0,
      title: false
    };
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex = null;
        this.answered = false;
        this.shuffleAnswers();
      }
    }
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index;
    },
    submitAnswer() {
      let isCorrect = false;

      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true;
        this.countCorrect++;
      }

      this.answered = true;
      this.countModalQuestion++;
      this.increment(isCorrect);
    },
    resetQuestions() {
      this.countCorrect = 0;
      this.countModalQuestion = 0;
      this.title = false;
      this.resetQuestion();
    },
    shuffleAnswers() {
      let answers = [
        ...this.currentQuestion.incorrect_answers,
        this.currentQuestion.correct_answer
      ];
      this.shuffledAnswers = _.shuffle(answers);
      this.correctIndex = this.shuffledAnswers.indexOf(
        this.currentQuestion.correct_answer
      );
    },
    answerClass(index) {
      let answerClass = "";

      if (!this.answered && this.selectedIndex === index) {
        answerClass = "selected";
      } else if (this.answered && this.correctIndex === index) {
        answerClass = "correct";
      } else if (
        this.answered &&
        this.selectedIndex === index &&
        this.correctIndex !== index
      ) {
        answerClass = "incorrect";
      }

      return answerClass;
    },
    modal() {
      if (this.countModalQuestion === 10) {
        return this.$bvModal.show("#modal-1");
      }
    },
    decoder(str) {
      var textArea = document.createElement("textarea");
      textArea.innerHTML = str;
      return textArea.value;
    }
  }
};
</script>

<style scoped>
div {
  margin-top: -3px;
}

.jumbotron {
  border-top-left-radius: 0;
  border-top-right-radius: 0;
  padding-top: 10px;
  margin-bottom: 15px;
  padding-bottom: 20px;
}

.list-group {
  margin-bottom: 15px;
}

.list-group-item {
  margin-bottom: 5px;
  border-radius: 4px;
}

.list-group-item:hover {
  background-color: #eee;
  cursor: pointer;
}

.btn {
  margin: 0 5px;
}

.selected {
  background-color: lightblue;
}

.correct {
  background-color: lightgreen;
}

.incorrect {
  background-color: red;
}

.kategori {
  text-decoration: underline;
  position: relative;
  text-underline-position: under;
  margin-top: 0;
  margin-bottom: 10px;
  padding-bottom: 10px;
}
</style>
