<template>
  <div ref="headerImage" class="relative white">
    <video
      poster="images/feature-eyf.jpg"
      class="w-100 h-100 db m"
      autoplay
      muted
      loop
      playsinline
      disablePictureInPicture
    >
      <source src="images/feature-eyf.webp" type="video/webp" />
      <source src="images/feature-eyf.mp4" type="video/mp4" />
    </video>
    <div class="absolute left-0 top-0 right-0 bottom-0 bg-black-40" />

    <div class="absolute bottom-0 text-shadow w-100">
      <div class="mw8 center pb4-ns ml5 tc">
        <h1 class="lh-title days-sans f-5-ns f3">
          {{ headerData.title }}
        </h1>
        <h2 class="lh-title f5 f3-ns mb0 normal">by {{ headerData.author }}</h2>
        <h5 class="lh-title f7 f4-ns mt0 normal">
          {{ headerData.publishDate }}
        </h5>
      </div>
    </div>
    <div v-if="headerData.imageCaption" class="image-caption">
      <span> {{ headerData.imageCaption }}</span>
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
