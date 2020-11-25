<template>
  <swiper-slide class="relative">
    <div class="absolute w-100 h-100 z--1 o-30">
      <video class="db w-100" autoplay loop muted playsinlines>
        <source :src="`${scenario.image}.webm`" />
        <source :src="`${scenario.image}.mp4`" />
        <img class="db w-100" :src="`${scenario.image}.gif`" />
      </video>
    </div>
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
    <article class="lh-copy absolute left-0 top-3 green">
      <div class="measure ph3 pv1 bg-black shadow br4">
        <div v-html="scenario.response.text"></div>
        <div>{{ scenario.option.a.content }}</div>
        <div>▓▓▓▓▓▓▓▓▓▓▓▓▓▓ 3.9%</div>
        <div>{{ scenario.option.b.content }}</div>
        <div>▓▓▓▓▓▓ 1.9%</div>
      </div>
      <div class="ph3">
        <p>NEXT SCENARIO ></p>
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

<style lang="scss" scoped>
@import '~@/assets/css/variables';

.shadow {
  box-shadow: 5px 5px 5px $green;
}
</style>
