<template>
  <div class="container">
    <div class="quiz-question">
      <h3> {{ questionSet.question }} </h3>
    </div>
    <div
      v-if="!hasVoted"
      class="quiz-answers"
    >
      <button
        v-for="option in questionSet.options"
        :key="option.title"
        @click="submitVote(option)"
      >
        {{ option.title }}
      </button>
    </div>
    <div
      v-else
      class="quiz-result"
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
  display: flex;
  flex-direction: column;
  @include breakpoint(medium) {
    flex-direction: row;
  }
}

h3 {
  padding: 1rem;
  font-weight: 800;
  text-align: center;
}

.quiz-question {
  display: flex;
  place-content: center;
  flex-basis: 70%;
  background-color: $darkblue;
  color: white;
  border-radius: 0.5rem;
  padding: 1rem;
  margin: 0.5rem;
}

.quiz-answers {
  display: flex;
  justify-content: center;
  @include breakpoint(medium) {
    flex-direction: column;
  }
  //First button
  button {
    flex-basis: 50%;
    text-align: center;
    background: unset;
    border: 0.5rem solid $darkblue;
    border-radius: 0.5rem;
    font-size: 1rem;
    font-weight: 300;
    margin: 0.5rem;
  }
}
</style>
