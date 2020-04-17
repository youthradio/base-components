<template>
  <div
    ref="headerImage"
    class="feature-container"
  >
    <video
      autoplay
      loop
      muted
      playsinline
      class="img-fluid video-float"
    >
      <source
        :src="`./${headerData.featureImage}.ogv`"
        type="video/ogv"
      >
      <source
        :src="`./${headerData.featureImage}.webm`"
        type="video/webm"
      >
      <source
        :src="`./${headerData.featureImage}.mp4`"
        type="video/mp4"
      >
      <a :href="`./${headerData.featureImage}.gif`">No support </a>
    </video>
    <!-- <img
      src="~./assets/blank.jpg"
      height="115px"
      width="1640px"
      alt="Elva dressed as a fairy"
      class="img-fluid lazyload"
      @load="updateHeaderHeight"
    > -->
    <div class="base-header title">
      <h3> {{ headerData.suptitle }}</h3>
      <h1 v-html="headerData.title" />
      <h3> {{ headerData.subtitle }}</h3>

      <!-- <h3> by {{ headerData.author }}</h3>
      <h5> {{ headerData.publishDate }}</h5> -->
    </div>
  </div>
</template>

<script>
export default {
  props: {
    headerData: {
      type: Object,
      require: true,
      default: null
    }
  },
  data () {
    return {
      innervalue: null
    }
  },
  methods: {
    updateHeaderHeight () {
      this.$emit('onHeaderImgHeight', this.$refs.headerImage.getBoundingClientRect().height)
    }
  }

}
</script>

<style lang="scss" scoped>
@import "~@/css/vars";
@import "~@/css/mixins";

.video-float {
  position: absolute;
  top: 0;
}
.img-fluid {
  max-width: 100%;
  width: 100%;
  height: auto;
  object-fit: cover;
}
.feature-container {
  position: relative;
  display: flex;
  flex-direction: column;
  background-color: $darkblue;
  padding-bottom: 56.25%;
  height: 0;
  background: radial-gradient(circle at 25% 10%, #292e49 20%, transparent 100%),
    radial-gradient(circle at 70% 30%, #6b5b67 50%, transparent 100%),
    radial-gradient(at 30% 50%, #332849 20%, transparent 100%),
    radial-gradient(at 70% 90%, #18102c 20%, white 100%);
}
.base-header {
  position: absolute;
  display: flex;
  place-items: center;
  place-content: center;
  flex-direction: column;
  width: 100%;
  height: 100%;
}
.title {
  h1,
  h2,
  h3 {
    font-family: "Assistant";
    font-style: normal;
    font-weight: 500;
    color: $white;
    text-shadow: 0px 0px 20px black;
  }
  h3 {
    font-size: 1.2rem;
    @include breakpoint(medium) {
      font-size: 1.5rem;
    }
    &:first-of-type {
      margin-left: -30%;
    }
    &:last-of-type {
      margin-right: -30%;
    }
  }
  h1 {
    padding: 0;
    text-transform: uppercase;
    font-size: 5rem;
    line-height: 3.5rem;
    @include breakpoint(medium) {
      font-size: 6rem;
      line-height: 4.5rem;
    }
    font-weight: 800;
    /deep/ span {
      &::before {
        content: "\A";
        white-space: pre;
      }
    }
  }
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
    font-family: "Roboto Mono", sans-serif;
    text-align: center;
    color: $blue-button;
  }
}
</style>
