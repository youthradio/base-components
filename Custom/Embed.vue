<template>
  <div
    v-observe-visibility="{
      callback: visibilityChanged,
      once: true,
    }"
    class="container"
    @mouseenter="mouseEventHand"
    @mouseleave="mouseEventHand"
  >
    <div ref="embed" v-html="htmlContent" />
  </div>
</template>

<script>
export default {
  props: {
    postData: {
      type: Object,
      require: true,
      default: null,
    },
  },
  data() {
    return {
      isVisible: false,
      isReady: false,
    }
  },
  computed: {
    htmlContent() {
      return this.postData.embed.cleanhtml
    },
    className() {
      return this.postData.embed.classname
    },
  },
  methods: {
    mouseEventHand(event) {
      if (event.type === 'mouseenter') {
        this.$emit('mouseActive', { postData: this.postData, event: 'enter' })
      } else if (event.type === 'mouseleave') {
        this.$emit('mouseActive', { postData: this.postData, event: 'leave' })
      }
    },
    visibilityChanged(isVisible, entry) {
      this.isVisible = isVisible
      if (entry.isIntersecting && !this.isReady) {
        this.isReady = true
        const el = this.$refs.embed.querySelector('.embed-class')
        el.classList.add(this.className) // add provider class
        this.$emit('onLoadEmbed', {
          provider: this.postData.embed.provider_name,
          el,
          entry,
        })
        // send visibility event, with element node and provider name, now we can trigger provider render script
      }
    },
  },
}
</script>

<style lang="scss" scoped>
/deep/ .instagram-media {
  max-width: 375px !important;
  margin-left: auto !important;
  margin-right: auto !important;
  margin-top: 0px !important;
  overflow-y: hidden !important;
}
/deep/ .twitter-tweet {
  width: 100% !important;
  max-width: 375px !important;
  margin-left: auto !important;
  margin-right: auto !important;
  margin-top: 0px !important;
  overflow-y: hidden !important;
}
/deep/ .tiktok-embed {
  width: 100% !important;
  max-width: 375px !important;
  margin-left: auto !important;
  margin-right: auto !important;
  margin-top: 0px !important;
  overflow-y: hidden !important;
}
/deep/ .embed-class {
  width: 100% !important;
  max-width: 375px !important;
  margin-left: auto !important;
  margin-right: auto !important;
  margin-top: 0px !important;
  overflow-y: hidden !important;
}
</style>
