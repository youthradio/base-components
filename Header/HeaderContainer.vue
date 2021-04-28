<template>
  <header>
    <component
      :is="headerType"
      v-bind="{ 'header-data': headerData, mode: mode }"
      @onHeaderImgHeight="setHeaderHeight"
    />

    <MenuHeader :offset="headerImageHeight" />
  </header>
</template>

<script>
import POSTCONFIG from '../../post.config'
import MenuHeader from './MenuHeader'
import FeatureHeader from './FeatureHeader'
import FeatureHeaderVideo from './FeatureHeaderVideo'
import FeatureHeaderCenter from './FeatureHeaderCenter'

export default {
  name: 'HeadContainer',
  components: {
    // eslint-disable-next-line vue/no-unused-components
    FeatureHeader,
    FeatureHeaderVideo,
    FeatureHeaderCenter,
    MenuHeader,
  },
  props: {
    mode: {
      type: String,
      required: false,
      default: 'base',
    },
    headerType: {
      type: String,
      required: false,
      default: 'FeatureHeader',
    },
  },
  data() {
    return {
      headerImageHeight: 0,
    }
  },
  computed: {
    headerData() {
      return {
        featureImage: POSTCONFIG.featureImagePath,
        title: POSTCONFIG.title,
        author: POSTCONFIG.author,
        imageCaption: POSTCONFIG.featureImageCaption,
        publishDate: POSTCONFIG.publishDate,
        location: POSTCONFIG.location,
      }
    },
  },
  created() {},
  mounted() {},
  methods: {
    setHeaderHeight(val) {
      this.headerImageHeight = val
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@import '~@/css/_vars';
header {
  // margin-bottom: 1rem;
}
</style>
