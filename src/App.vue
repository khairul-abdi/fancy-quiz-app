<template>
  <div id="app" class="containers">
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <Header
            :countCorrect="countCorrect"
            :totalQuestion="questions.length"
            :countQuestion="questions.length ? index + 1 : index"
          />
        </b-col>
      </b-row>
    </b-container>

    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <Menu :fetchApi="fetchApi"/>
        </b-col>

        <b-col sm="6" offset="3" v-if="selectedOption && !questions.length">
          <Loading/>
        </b-col>

        <b-col sm="6" offset="3" v-else>
          <QuestionBox
            v-if="questions.length"
            :currentQuestion="questions[index]"
            :selectedOption="selectedOption"
            :next="next"
            :increment="increment"
            :resetQuestion="resetQuestion"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Menu from "./components/Menu.vue";
import Header from "./components/Header.vue";
import QuestionBox from "./components/QuestionBox.vue";
import Loading from "./components/Loading.vue";

export default {
  name: "App",
  components: {
    Menu,
    Header,
    QuestionBox,
    Loading
  },
  data() {
    return {
      questions: [],
      index: 0,
      countCorrect: 0,
      selectedOption: "",
      api: "https://opentdb.com/api.php?amount=10&type=multiple"
    };
  },
  methods: {
    next() {
      this.index++;
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.countCorrect++;
      }
    },
    fetchApi(api, name) {
      this.selectedOption = name;
      if (api) {
        this.api = api;
        this.loadData();
      }
    },
    resetQuestion() {
      this.questions = [];
      this.countCorrect = 0;
      this.index = 0;
    },
    loadData() {
      fetch(this.api, {
        method: "get"
      })
        .then(response => {
          return response.json();
        })
        .then(jsonData => {
          this.questions = jsonData.results;
        });
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
}

div {
  text-align: center;
}
</style>
