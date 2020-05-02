<template>
  <div class="question-box-container">
    <b-jumbotron>
      <template v-slot:lead>
        <span v-html="question.question" />
      </template>

      <hr class="my-4" />

      <b-list-group class="mb-3">
        <b-list-group-item
          v-for="(answer, index) in shuffledAnswers"
          :key="index"
          @click.prevent="selectIndex(index)"
          :class="answerClass(index)"
          >{{ answer }}</b-list-group-item
        >
      </b-list-group>

      <b-button
        variant="primary"
        @click="submitAnswer"
        :disabled="selectedIndex === null || isAnswered"
        >Submit</b-button
      >
      <b-button @click="next" variant="success">Next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
import _ from "lodash";
export default {
  props: {
    question: Object,
    next: Function,
    increment: Function,
  },
  data() {
    return {
      shuffledAnswers: [],
      selectedIndex: null,
      isAnswered: false,
    };
  },
  computed: {
    answers() {
      let answers = [...this.question.incorrect_answers];
      answers.push(this.question.correct_answer);
      //   answers = ["hello", "world"];
      return answers;
    },
  },
  watch: {
    question: {
      immediate: true,
      handler() {
        console.log("watcher in qb ran...");
        this.selectedIndex = null;
        this.isAnswered = false;
        this.shuffleAnswers();
      },
    },
  },
  methods: {
    selectIndex(index) {
      this.selectedIndex = index;
    },
    shuffleAnswers() {
      let answers = [
        ...this.question.incorrect_answers,
        this.question.correct_answer,
      ];
      this.shuffledAnswers = _.shuffle(answers);
    },
    submitAnswer() {
      this.increment(
        this.shuffledAnswers[this.selectedIndex] ===
          this.question.correct_answer
      );
      this.isAnswered = true;
    },
    answerClass(index) {
      return !this.isAnswered && this.selectedIndex === index
        ? "selected"
        : this.isAnswered &&
          this.shuffledAnswers[index] === this.question.correct_answer
        ? "correct"
        : this.isAnswered &&
          this.selectedIndex === index &&
          this.shuffledAnswers[index] !== this.question.correct_answer
        ? "incorrect"
        : "";
    },
  },
};
</script>

<style scoped>
.btn {
  margin: 0 6px;
}
.list-group-item:hover {
  background-color: #eee;
  cursor: pointer;
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
</style>
