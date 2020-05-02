<template>
  <div id="app">
    <Header :numCorrect="numCorrect" :numTotal="numTotal" />

    <b-container>
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBox
            v-if="questions.length"
            :question="questions[index]"
            :next="next"
            :increment="increment"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import QuestionBox from "./components/Question-Box.vue";

export default {
  name: "App",
  components: {
    Header,
    QuestionBox,
  },
  data() {
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0,
    };
  },
  methods: {
    next() {
      this.index++;
    },
    increment(isCorrect) {
      if (isCorrect) this.numCorrect++;
      this.numTotal++;
    },
  },
  mounted: function() {
    fetch("https://opentdb.com/api.php?amount=10&category=19&type=multiple", {
      method: "get",
    })
      .then((res) => res.json())
      .then((resdata) => {
        console.log(resdata.results);
        this.questions = resdata.results;
      })
      .catch((err) => console.log(err));
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
