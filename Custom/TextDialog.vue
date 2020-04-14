<template>
  <div ref="container">
    <div
      v-for="dialog in dialogs"
      :key="dialog.text"
      class="dialog"
    >
      <div class="speaker-name col-l">
        {{ dialog.name }}
      </div>
      <div
        class="text col-r"
        v-html="dialog.text"
      />
    </div>
  </div>
</template>

<script>

export default {
  props: {
    dialogs: {
      type: Array,
      require: true,
      default: null

    }
  },
  data () {
    return {

    }
  },
  computed: {

  },
  mounted () {

  },
  methods: {

  }
}
</script>

<style lang="scss" scoped>
@import "~@/css/mixins";

.dialog {
  display: grid;
  grid-template-columns: 1fr 3fr;
  grid-template-areas: "left right";
  column-gap: 1rem;

  .col-l {
    grid-area: left;
  }
  .col-r {
    grid-area: right;
  }
  .text {
    font-size: 0.8rem;
  }
  .speaker-name {
    font-family: "Roboto Mono";
    font-weight: bold;
    text-align: right;
  }
}
</style>
