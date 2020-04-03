<template>
  <div class="container">
    <div class="quiz-question">
      <h3> {{ questionSet.question }} </h3>
    </div>
    <div v-if="!hasVoted" class="quiz-answers">
      <button @click="submitVote('A')">
        {{ questionSet.A }}
      </button>
      <button @click="submitVote('B')">
        {{ questionSet.B }}
      </button>
    </div>
    <div v-else class="quiz-result">
      Test
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
      this.selectedButton = vote
      this.hasVoted = true
    }
  }
}
</script>
<style lang="scss" scoped>
@import "~@/css/mixins";
@import "~@/css/vars";

</style>
