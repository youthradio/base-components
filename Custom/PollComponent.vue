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
      <div class="content">
        <strong> {{ result.total }}% </strong>
        choose {{ result.title }}
      </div>
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
      hasVoted: false,
      result: null
    }
  },
  mounted () {
  },
  methods: {
    async submitVote (vote) {
      const res = await fetch(
        `https://ee51aej7u4.execute-api.us-west-2.amazonaws.com/latest/vote_poll/${this.questionSet.id}/${vote.id}`,
        {
          method: 'GET',
          credentials: 'include'
        }
      ).then(res => res.json())
      const total = res.poll.options.reduce((a, i) => a + i.count, 0) // adds total counts
      const selectedVote = res.poll.options.find(i => i.id === vote.id) // find count for voted option
      const percentage = 100 * selectedVote.count / total
      this.result = {
        total: percentage.toFixed(),
        title: vote.title
      }
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
  color: $white;
  border-radius: 0.5rem;
  padding: 1rem;
  margin: 0.5rem;
}
.quiz-result {
  flex-basis: 30%;
  display: flex;
  flex-grow: 1;
  place-items: center;
  background-color: $lightgrey;
  border-radius: 0.5rem;
  padding: 1rem;
  margin: 0.5rem;

  .content {
    margin: auto;
    font-size: larger;
  }
}

.quiz-answers {
  display: flex;
  justify-content: center;
  flex-basis: 30%;
  @include breakpoint(medium) {
    flex-direction: column;
  }
  //First button
  button {
    cursor: pointer;
    flex-basis: 50%;
    text-align: center;
    background: unset;
    border: 0.2rem solid $darkblue;
    border-radius: 0.5rem;
    font-size: 1rem;
    font-weight: 300;
    margin: 0.5rem;
  }
}
</style>
