<template>
  <div class="container">
    <div v-html="htmlContent" />
  </div>
</template>

<script>
export default {
  props: {
    postData: {
      type: Object,
      require: true,
      default: null
    }
  },
  data () {
    return {

    }
  },
  computed: {
    htmlContent () {
      return this.postData.embed.cleanhtml
    }
  },
  methods: {

  }
}
</script>

<style lang="scss" scoped>
/deep/ .instagram-media {
  max-width: 375px !important;
}
/deep/ .twitter-tweet {
  width: 100% !important;
  max-width: 375px !important;
}
/deep/ .tiktok-embed {
  width: 100% !important;
  max-width: 375px !important;
}
/deep/ .embed-class {
  width: 100% !important;
  max-width: 375px !important;
  margin-left: auto !important;
  margin-right: auto !important;
}
</style>
