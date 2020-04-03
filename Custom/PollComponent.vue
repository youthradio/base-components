<template>
  <div class="container">
    <div class="quiz-question">
      <h3> {{ questionSet.question }} </h3>
    </div>
    <div class="quiz-answers">
      <button>{{ questionSet.A }}</button>
      <button>{{ questionSet.B }}</button>
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
  mounted () {
  }
}
</script>
<style lang="scss" scoped>
@import "~@/css/mixins";
@import "~@/css/vars";

</style>
