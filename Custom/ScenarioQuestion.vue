<template>
  <swiper-slide class="relative">
    <div class="absolute w-100 h-100 z--1 o-30">
      <video
        class="db w-100"
        autoplay
        loop
        muted
        playsinlines
        :poster="`${scenario.image}.jpg`"
      >
        <source :src="`${scenario.image}.mp4`" />
        <source :src="`${scenario.image}.webp`" />
      </video>
    </div>
    <article class="measure lh-copy ph3 relative">
      <div class="bg-green br4 ph3 pv1" v-html="scenario.prompt.text"></div>
      <div class="flex justify-center mt3">
        <button
          :disabled="toggled"
          class="bn pointer black bg-green br4 db pa1 ph2 grow mh2 tc"
          @click.prevent="processOption(scenario.option.id)"
        >
          <span>{{ scenario.option.a.content }}</span>
        </button>
        <button
          :disabled="toggled"
          class="bn pointer black bg-green br4 db pa1 ph2 grow mh2 tc"
          @click.prevent="processOption(scenario.option.id)"
        >
          <span>{{ scenario.option.b.content }}</span>
        </button>
      </div>
    </article>
    <article
      v-if="toggled"
      ref="modal"
      class="lh-copy absolute left-0 top-3 green ph3"
      @click="toggled = !toggled"
    >
      <div class="measure ph3 pv1 bg-black shadow br4">
        <div v-html="scenario.response.text"></div>
        <div>{{ scenario.option.a.content }}</div>
        <div>▓▓▓▓▓▓▓▓▓▓▓▓▓▓ 3.9%</div>
        <div>{{ scenario.option.b.content }}</div>
        <div>▓▓▓▓▓▓ 1.9%</div>
      </div>
      <div class="ph3">
        <button
          class="bn pointer green db grow mt2 bg-inherit"
          @click.prevent="
            $emit('next-page', next)
            toggled = !toggled
          "
        >
          {{ next ? 'NEXT SCENARIO >' : 'CONCLUSION >' }}
        </button>
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
      required: true,
      default: () => {},
    },
    next: {
      type: Number,
      required: true,
      default: 0,
    },
  },
  data() {
    return {
      toggled: false,
    }
  },
  methods: {
    processOption(optionid) {
      this.toggled = true
    },
  },
}
</script>

<style lang="scss" scoped>
@import '~@/assets/css/variables';

.shadow {
  box-shadow: 5px 5px 5px $green;
}
</style>
