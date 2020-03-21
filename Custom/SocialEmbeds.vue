<template>
  <div class="container">
    <h1> TEsting</h1>
    <div v-html="embedsData.slice(0,10).map(e=>e.embed.cleanhtml).join('')" />
  </div>
</template>

<script>
import * as d3require from 'd3-require'
export default {
  props: {
    embedsData: {
      type: Array,
      require: true,
      default: null
    }
  },
  data () {
    return {
      twttr: null,
      instgrm: null,
      tiktokEmbed: null
    }
  },
  computed: {

  },
  created () {
    this.getScripts()
  },
  mounted () {

  },
  methods: {
    async getScripts () {
      this.twttr = await d3require.require('https://platform.twitter.com/widgets.js').catch(
        () => window.twttr)
      this.instgrm = await d3require.require('https://instagram.com/embed.js').catch(
        () => window.instgrm
      )
      this.tiktokEmbed = await d3require.require('https://www.tiktok.com/embed.js').catch(() => window.tiktokEmbed)
    }
  }
}
</script>

<style lang="scss" scoped>

/deep/ .instagram-media {
  max-width: 375px!important;
}
/deep/ .twitter-tweet {
  width: 100% !important;
  max-width: 375px!important;
}
/deep/ .tiktok-embed {
  width: 100% !important;
  max-width: 375px !important;
}
</style>
