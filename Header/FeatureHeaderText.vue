<template>
  <div
    ref="headerImage"
    class="feature-container"
  >
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

.img-fluid {
  max-width: 100%;
  width: 100%;
  height: auto;
  object-fit: cover;
  max-height: 80vh;
}
.feature-container {
  position: relative;
  height: 100vh;
  display: flex;
  flex-direction: column;
  background-color: $grey;
  // height: 80vh;
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
    font-weight: 300;
  }
  h3 {
    font-size: 1rem;
    @include breakpoint(medium) {
      font-size: 1.5rem;
    }
    &:first-of-type {
      margin-left: -40%;
    }
    &:last-of-type {
      margin-right: -40%;
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
