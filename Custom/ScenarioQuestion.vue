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
          @click.prevent="processOption(scenario.option.a.id)"
        >
          <span>{{ scenario.option.a.content }}</span>
        </button>
        <button
          :disabled="toggled"
          class="bn pointer black bg-green br4 db pa1 ph2 grow mh2 tc"
          @click.prevent="processOption(scenario.option.b.id)"
        >
          <span>{{ scenario.option.b.content }}</span>
        </button>
      </div>
    </article>
    <article
      v-if="toggled"
      ref="modal"
      class="lh-copy absolute top-3 green ph3"
      @click="toggled = !toggled"
    >
      <div class="measure pa3 bg-black shadow br4">
        <div v-html="scenario.response.text"></div>
        <div>
          <div>{{ scenario.option.a.content }}</div>
          <div v-if="result">{{ generateState(result.a) }}</div>
          <div v-else class="fadein-loading">██████ %</div>
          <div>{{ scenario.option.b.content }}</div>
          <div v-if="result">{{ generateState(result.b) }}</div>
          <div v-else class="fadein-loading">██████ %</div>
        </div>
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
import { POLLSERVER } from '~/post.config'

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
      voteLoading: false,
      result: null,
    }
  },
  methods: {
    generateState(val) {
      const CHAR = '▓'
      const stat = Array(~~(15 * val))
        .fill(CHAR)
        .join('')
      return `${stat} ${(100 * val).toFixed()}%`
    },
    async processOption(voteid) {
      this.toggled = true
      this.voteLoading = true

      const res = await fetch(
        `${POLLSERVER}/vote_poll/${this.scenario.option.id}/${voteid}`,
        {
          method: 'GET',
          credentials: 'include',
        }
      ).then((res) => res.json())
      const total = res.poll.options.reduce((a, i) => a + i.count, 0) // adds total counts
      const votes = Object.fromEntries(
        res.poll.options.map((e) => [e.id, e.count])
      )
      this.result = {
        a: votes[this.scenario.option.a.id] / total,
        b: votes[this.scenario.option.b.id] / total,
      }
      this.voteLoading = false
    },
  },
}
</script>

<style lang="scss" scoped>
@import '~@/assets/css/variables';

.shadow {
  box-shadow: 5px 5px 5px $green;
}
@keyframes fadein {
  from {
    opacity: 0.2;
  }
}

.fadein-loading {
  animation: fadein 1s infinite alternate;
}
</style>
