<template>
  <div class="container">
    <div class="quiz-question">
      <h3>{{ questionSet.question }}</h3>
    </div>
    <div class="quiz-answers">
      <button
        v-for="option in questionSet.options"
        :key="option.title"
        :style="{ visibility: hasVoted ? 'hidden' : '' }"
        @click="submitVote(option)"
      >
        {{ option.title }}
      </button>
      <div v-if="hasVoted" class="quiz-result">
        <div class="content">
          <strong> {{ result.total }}% </strong>
          chose {{ result.title }}
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import POSTCONFIG from '~/post.config'

export default {
  props: {
    questionSet: {
      type: Object,
      required: true,
      default: null
    }
  },
  data() {
    return {
      hasVoted: false,
      result: null
    }
  },
  mounted() {},
  methods: {
    async submitVote(vote) {
      const res = await fetch(
        `${POSTCONFIG.POLLSERVER}/vote_poll/${this.questionSet.id}/${vote.id}`,
        {
          method: 'GET',
          credentials: 'include'
        }
      ).then((res) => res.json())
      const total = res.poll.options.reduce((a, i) => a + i.count, 0) // adds total counts
      const selectedVote = res.poll.options.find((i) => i.id === vote.id) // find count for voted option
      const percentage = (100 * selectedVote.count) / total
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
@import '~@/css/mixins';
@import '~@/css/vars';

.container {
  display: flex;
  flex-direction: column;
  @include breakpoint(medium) {
    flex-direction: row;
  }
}

h3 {
  padding: 1rem;
  letter-spacing: 0;
  font-weight: 800;
  text-align: center;
  margin: auto;
}

.quiz-question {
  display: flex;
  place-content: center;
  flex-basis: 60%;
  background-color: $darkblue;
  color: $white;
  border-radius: 0.5rem;
}
.quiz-result {
  position: absolute;
  width: 100%;
  height: 100%;

  display: flex;
  flex-grow: 1;
  place-items: center;
  background-color: $lightpurple;
  color: $white;
  border-radius: 0.5rem;
  text-align: center;
  .content {
    margin: auto;
    padding: 1rem;
    font-size: larger;
  }
}

.quiz-answers {
  position: relative;
  display: flex;
  justify-content: center;
  flex-basis: 40%;
  margin-top: 0.5rem;

  @include breakpoint(medium) {
    flex-direction: column;
    margin-left: 0.5rem;
    margin-top: 0;
  }
  //First button
  button {
    font-family: 'Assistant', Arial, Helvetica, sans-serif;
    cursor: pointer;
    flex-basis: 50%;
    text-align: center;
    background: unset;
    border: 0.2rem solid $darkblue;
    border-radius: 0.5rem;
    font-size: 1rem;
    font-weight: 300;
    min-height: 3.5rem;
    &:hover {
      background-color: $lightpurple;
      color: $white;
    }

    &:nth-of-type(1) {
      margin-right: 0.25rem;
      @include breakpoint(medium) {
        margin-bottom: 0.25rem;
        margin-right: 0;
      }
      &:active {
        transform: translateY(5px);
      }
    }
    &:nth-of-type(2) {
      margin-left: 0.25rem;
      @include breakpoint(medium) {
        margin-left: 0;
        margin-top: 0.25rem;
      }
    }
    &:active {
      transform: translateY(-5px);
    }
  }
}
</style>
