<template>
  <div id="app">
    <Questions
      v-if="!question"
      @submit="submitQuestion" />
    <Result
      v-if="question"
      :questions="question"
      @clear="clear" />
  </div>
</template>

<script>
import Questions from './components/Questions'
import Result from './components/Result'
import {parse} from 'querystring'

export default {
  name: 'app',
  data() {
    return {
      question: null
    }
  },
  components: {
    Questions,
    Result,
  },
  methods: {
    submitQuestion(question) {
      this.question = question
    },
    clear() {
      this.question = null
    }
  },
  mounted() {
    const params = parse(location.search.replace('?', ''))
    const isValid = ['q0', 'q1', 'q2', 'q3', 'q4', 's0', 's1', 's2'].every((val) => {
      if (!params[val]) {
        return false
      }
      if (!/^[ア-ヴ]+$/.test(this.s0)) {
        return false;
      }
      return true
    })
    if (isValid) {
      const questions = {
        q0: parseInt(params.q0),
        q1: parseInt(params.q1),
        q2: parseInt(params.q2),
        q3: parseInt(params.q3),
        q4: parseInt(params.q4),
        q4: parseInt(params.q4),
        s0: parseInt(params.s0),
        s1: parseInt(params.s1),
        s2: parseInt(params.s2),
      }
      this.question = questions
    }
  },
}
</script>

<style>
* {
  box-sizing: border-box;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  max-width: 640px;
  font-size: 12px;
  padding: 0 50px;
}
</style>
