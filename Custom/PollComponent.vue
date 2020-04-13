<template>
  <div class="container">
    <div class="quiz-question flex-item">
      <h3> {{ questionSet.question }} </h3>
    </div>
    <div
      v-if="!hasVoted"
      class="quiz-answers flex-item"
    >
      <button @click="submitVote('A')">
        {{ questionSet.options[0].title }}
      </button>
      <button @click="submitVote('B')">
        {{ questionSet.options[1].title }}
      </button>
    </div>
    <div
      v-else
      class="quiz-result flex-item"
    >
      You selected {{ selectedButton }}!
    </div>
  </div>
</template>
<script>
export default {
  props: {
    questionSet: {
      type: Object,
      required: true,
      default: null
    }
  },
  data () {
    return {
      selectedButton: null,
      hasVoted: false
    }
  },
  mounted () {
  },
  methods: {
    submitVote (vote) {
      // maybe an async function has to sit between the end of this function and changing the data to calculate a percentage of people who've voted for what? maybe an api'll handle that for us?
      this.selectedButton = vote
      this.hasVoted = true
    }
  }
}
</script>
<style lang="scss" scoped>
@import "~@/css/mixins";
@import "~@/css/vars";

.container {
  padding-top: 1rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  * {
    font-size: 100%;
  }
  .flex-item {
    margin: 0rem 0rem 1rem 0rem;
    flex-grow: 1;
    flex-basis: 0;
  }
  h3 {
    padding: 0;
    font-weight: 800;
  }
  @include breakpoint(medium) {
    flex-direction: row;
    .flex-item {
      margin: 0 1rem 0 1rem;
    }
  }
}

.quiz-question {
  background-color: #332849;
  color: white;
  text-align: center;
  border-radius: 5px;
  padding: 1rem;
}

.quiz-answers {
  display: flex;
  flex-direction: row;
  justify-content: center;

  //First button
  button {
    background: transparent;
    border: 5px solid #332849;
    border-radius: 5px;
    margin: 0rem 0.3rem 0rem 0;
    width: 100%;
    flex-grow: 1;
    flex-basis: 0;
    font-weight: 300;
  }
  //Second button
  button + button {
    margin: 0rem 0 0rem 0.3rem;
  }

  @include breakpoint(medium) {
    display: flex;
    flex-direction: column;
    justify-content: center;
    button {
      margin: 0rem 0 0.3rem 0;
    }
    //Second button
    button + button {
      margin: 0.3rem 0 0rem 0;
    }
  }
}
</style>
