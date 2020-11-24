<template>
  <swiper-slide class="relative">
    <div
      class="absolute w-100 h-100"
      :style="{
        backgroundImage: `url(${scenario.image}.gif)`,
        backgroundPosition: 'center',
        backgroundSize: 'cover',
      }"
    ></div>
    <article class="measure lh-copy ph3 relative">
      <div class="bg-green br4 ph3 pv1" v-html="scenario.prompt.text"></div>
      <div class="flex justify-center mt3">
        <a href="" class="no-underline black bg-green br4 db pa2 grow mh2 tc">
          <span>{{ scenario.option.a.content }}</span>
        </a>
        <a href="" class="no-underline black bg-green br4 db pa2 grow mh2 tc">
          <span>{{ scenario.option.b.content }}</span>
        </a>
      </div>
    </article>
  </swiper-slide>
</template>

<script>
import SwiperSlide from './SwiperSlide'

export default {
  name: 'ScenarioQuestion',
  components: {
    SwiperSlide,
  },
  props: {
    scenario: {
      type: Object,
      required: false,
      default: () => {},
    },
  },
  data() {
    return {}
  },
}
</script>

<style></style>
