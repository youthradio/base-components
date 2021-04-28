<template>
  <div ref="headerImage" class="relative white min-50vh">
    <div
      :style="{ backgroundImage: `url(${headerData.featureImage})` }"
      class="min-70vh text-shadow flex justify-center items-center z-1"
    >
      <h1 class="lh-title-1-1 daysans f1-ns f3 ma0 pa0 ttu">
        {{ headerData.title }}
      </h1>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    headerData: {
      type: Object,
      require: true,
      default: null,
    },
    mode: {
      type: String,
      required: false,
      default: 'base',
    },
  },
  data() {
    return {
      innervalue: null,
    }
  },
  methods: {
    updateHeaderHeight() {
      this.$emit(
        'onHeaderImgHeight',
        this.$refs.headerImage.getBoundingClientRect().height
      )
    },
  },
}
</script>

<style lang="scss" scoped>
@import '~@/css/vars';

.base-overlay::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 45%;
  background-color: rgba(lighten($feature-header-color, 20%), 0.8);
  z-index: 0;
}

.image-caption {
  position: absolute;
  width: 100%;
  text-align: center;
  bottom: -1rem;
  z-index: 1;
  span {
    font-weight: 400;
    font-size: 0.5rem;
    line-height: 1rem;
    font-family: 'Roboto Mono', sans-serif;
    text-align: center;
    color: $blue-button;
  }
}
.text-shadow {
  text-shadow: -1px 1px 2px black;
}
</style>
