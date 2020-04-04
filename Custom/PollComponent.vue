<template>
  <div class="container">
    <div class="quiz-question flex-item">
      <h3> {{ questionSet.question }} </h3>
    </div>
    <div v-if="!hasVoted" class="quiz-answers flex-item">
      <button @click="submitVote('A')">
        {{ questionSet.options[0].title }}
      </button>
      <button @click="submitVote('B')">
        {{ questionSet.options[1].title }}
      </button>
    </div>
    <div v-else class="quiz-result flex-item">
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
    flex-direction: row;
    justify-content: center;
    .flex-item{
        margin: 0 1rem 0 1rem;
        flex-grow: 1;
        flex-basis: 0;
    }
    h3 {
        padding: 0;
    }
}

.quiz-answers{
    display: flex;
    flex-direction: column;
    justify-content: center;

    button {
        background: transparent;
        border: 5px solid #332849;
        border-radius: 5px;
        padding: 0.5rem 0rem 0.5rem 0rem;
        margin: 0.3rem;

        font-weight: bold;
    }
}

</style>
