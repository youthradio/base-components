<template>
  <div class="auto-margin">
    <template
      v-if="topic.format === 'graphic'"
      class="template-container"
    >
      <article v-html="topic.text" />
    </template>
    <template
      v-else-if="topic.format === 'text'"
      class="template-container"
    >
      <article>
        <h1 class="header-title">
          {{ topic.title }}
        </h1>
        <h4
          v-if="topic.byline"
          class="by-line"
        >
          {{ topic.byline }}
        </h4>
      </article>
      <article v-html="topic.text" />
    </template>
    <template
      v-else-if="topic.format === 'video'"
      class="template-container"
    >
      <article>
        <h1 class="header-title">
          {{ topic.title }}
        </h1>
        <h4
          v-if="topic.byline"
          class="by-line"
        >
          {{ topic.byline }}
        </h4>
      </article>
      <article v-html="topic.text" />
      <article>
        <vue-plyr>
          <div class="plyr__video-embed">
            <iframe
              :src="`https://www.youtube.com/embed/${topic.link}?iv_load_policy=3&modestbranding=1&playsinline=1&showinfo=0&rel=0&enablejsapi=1`"
              allowfullscreen
              allowtransparency
              allow="autoplay"
            />
          </div>
        </vue-plyr>
      </article>
    </template>
    <template
      v-else-if="topic.format === 'audio'"
      class="template-container"
    >
      <article>
        <h1 class="header-title">
          {{ topic.title }}
        </h1>
        <h4
          v-if="topic.byline"
          class="by-line"
        >
          {{ topic.byline }}
        </h4>
      </article>
      <article>
        <vue-plyr>
          <audio>
            <source
              :src="topic.link"
              type="audio/mp3"
            >
          </audio>
        </vue-plyr>
      </article>
      <article v-html="topic.text" />
    </template>
  </div>
</template>

<script>
export default {
  props: {
    topic: {
      type: Object,
      require: true,
      default: null
    }
  },
  data () {
    return {

    }
  },
  computed: {

  },
  methods: {

  }
}
</script>

<style lang="scss" scoped>
.auto-margin > * {
  display: block;
  width: auto;
}

.img-fluid {
  width: 100%;
  height: auto;
}

.graphic {
  max-width: 32rem;
  margin: 0 auto;
  text-align: center;
}
.flex {
  display: flex;
}
.center {
  justify-content: center;
}
</style>
