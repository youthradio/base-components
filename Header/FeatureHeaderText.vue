<template>
  <div ref="headerImage" class="feature-container">
    <video autoplay loop muted playsinline class="img-fluid video-float">
      <source :src="`./${headerData.featureImage}.ogv`" type="video/ogv" />
      <source :src="`./${headerData.featureImage}.webp`" type="video/webp" />
      <source :src="`./${headerData.featureImage}.mp4`" type="video/mp4" />
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
    <div class="base-header">
      <div class="title">
        <h1 v-html="headerData.title" />
        <h3 v-html="headerData.subtitle" />
      </div>
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
      default: null,
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
@import '~@/css/mixins';

.video-float {
  position: absolute;
  top: 0;
}
.img-fluid {
  max-width: 100%;
  width: 100%;
  height: auto;
  object-fit: cover;
  max-height: 100vh;
}
.feature-container {
  position: relative;
  display: flex;
  flex-direction: column;
  background-color: $darkblue;
  padding-bottom: MIN(56.25%, 100vh);
  height: 0;
  background: radial-gradient(circle at 25% 10%, #292e49 20%, transparent 100%),
    radial-gradient(circle at 70% 30%, #6b5b67 50%, transparent 100%),
    radial-gradient(at 30% 50%, #332849 20%, transparent 100%),
    radial-gradient(at 70% 90%, #18102c 20%, white 100%);
}
.base-header {
  position: absolute;
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
}
.title {
  width: 100%;
  max-width: 35rem;
  padding-left: 1rem;
  padding-right: 1rem;
  margin: auto auto 2rem auto;
  h1,
  h2,
  h3 {
    color: $white;
    text-shadow: 0px 0px 20px black;
    letter-spacing: 0;
    /deep/ span {
      &::before {
        content: '\A';
        white-space: pre;
      }
    }
  }
  h3 {
    max-width: 85%;
    font-style: normal;
    font-weight: 500;
    font-size: 0.9rem;
    line-height: 1rem;
    padding-top: 1rem;
    padding-bottom: 0rem;
    @include breakpoint(medium) {
      font-size: 1rem;
      line-height: 1.4rem;
      padding-top: 1.5rem;
      padding-bottom: 1.5rem;
    }
  }
  h1 {
    padding: 0rem;
    text-transform: uppercase;
    line-height: 2rem;
    font-weight: 800;
    font-size: 2.5rem;
    @include breakpoint(medium) {
      line-height: 3.5rem;
      font-size: 4rem;
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
    font-family: 'Roboto Mono', Arial, Helvetica, sans-serif;
    text-align: center;
    color: $blue-button;
  }
}
</style>
