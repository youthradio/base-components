<template>
  <header class="article-header">
    <div
      v-if="headType === 'main'"
      :class="[headType === 'main' ? 'bg-container' : '']"
    >
      <img
        :data-srcset="
          `${headerImg}x300.jpg 375w,
        ${headerImg}x750.jpg 563w,
        ${headerImg}x1050.jpg 1125w,
        ${headerImg}x1350.jpg 1500w,
        ${headerImg}x1500.jpg 1875w,
        `
        "
        :data-src="`${headerImg}x1500.jpg`"
        alt="The golden gate bridge"
        class="img-fluid lazyload"
      />
    </div>
    <div
      :class="[
        headType === 'main' ? 'top-container title' : 'sub-container sub-title'
      ]"
    >
      <div v-if="headType === 'main'">
        <h1>{{ articleData.title }}</h1>
        <h3>{{ articleData.subtitle }}</h3>
      </div>
      <div v-if="headType === 'subpage'" class="headline-margins">
        <h2>
          {{ articleData.title }}
        </h2>
        <h3>
          {{ articleData.subtitle }}
        </h3>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  components: {},
  mixins: [],
  props: {
    articleData: {
      required: false,
      type: Object,
      default: null
    },
    headType: {
      required: false,
      type: String,
      default: 'main'
    }
  },
  data() {
    return {}
  },
  computed: {
    headerImg() {
      return this.articleData.featureImage.trim()
    }
  },
  watch: {},
  mounted() {}
}
</script>

<style lang="scss" scoped>
@import '~@/css/vars';

.sub-title,
.title {
  h1,
  h2,
  p {
    padding: 0;
  }
}
.article-header {
  position: relative;
}

.sub-container {
  background-color: $yellow;
  padding-top: 2.5rem;
  padding-bottom: 0.5rem;
}
.headline-margins {
  max-width: 40rem;
  margin-left: auto;
  margin-right: auto;
  padding-left: 1.5rem;
  padding-right: 1.5rem;
}
.top-container {
  width: 100%;
  text-align: center;
  z-index: 1;
  padding: 0.5rem;
  position: absolute;
  bottom: 0px;
}

.bg-container {
  z-index: 0;
  width: 100%;
  background-color: $yellow;
}
.img-fluid {
  opacity: 0.5;
  max-height: 800px;
  object-fit: cover;
  vertical-align: top;
}
</style>
