<template>
  <div
    ref="container"
    class="container"
  >
    <div
      class="tab-header sticky"
      :style="{backgroundColor: selectedCategory.color}"
    >
      <button
        v-for="category in embedsData.categories"
        :key="category.name"
        :style="[{backgroundColor: category.color}, selectedCategory.name === category.name ? ({fontWeight: 'bold'}):null]"
        class="tab-link"
        @click="setCategory(category)"
      >
        {{ category.name }}
      </button>
    </div>
    <div ref="line" />
    <div
      v-for="category in embedsData.categories"
      :key="category.name"
      class="embeds-container"
      :style="[
        {backgroundColor:selectedCategory.color},
        checkSelectedCategory(category)
      ]"
    >
      <Embed
        v-for="(post,id) in filteredEmbeds(category)"
        :key="post.user"
        ref="embedsRef"
        :data-refid="`${category.name}-${id}`"
        :post-data="post"
        @onLoadEmbed="onLoadEmbed"
        @mouseActive="mouseActive"
      />
    </div>
  </div>
</template>

<script>
import * as d3require from 'd3-require'
import Embed from './Embed.vue'

export default {
  components: {
    Embed
  },
  props: {
    embedsData: {
      type: Object,
      require: true,
      default: null
    }
  },
  data () {
    return {
      selectedCategory: null,
      twttr: null,
      instgrm: null,
      tiktokEmbed: null,
      currentActiveState: null
    }
  },
  computed: {

  },
  created () {
    this.getScripts()
    this.selectedCategory = this.embedsData.categories[0]
    this.$emit('onSelectCategory', this.selectedCategory)
    const initPost = this.filteredEmbeds(this.selectedCategory)[0]
    this.currentActiveState = { state: initPost.state, location: initPost.location }
    this.$emit('onActiveState', this.currentActiveState)
  },
  mounted () {
    // const windowHalf = window.innerHeight / 2
    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        this.checkEmbedMapLocation(entry.boundingClientRect, entry.target)
      })
    },
    {
      threshold: Array(50).fill().map((_, i) => i / 50)
    })
    this.$refs.embedsRef.map((e) => {
      observer.observe(e.$el)
    })
  },
  methods: {
    mouseActive ({ postData, event }) {
      if (event === 'enter') {
        this.$emit('onActiveState', { state: postData.state, location: postData.location })
      } else {
        this.$emit('onActiveState', this.currentActiveState)
      }
    },
    checkSelectedCategory (category) {
      return (this.selectedCategory.name !== category.name) ? { display: 'none' } : null
    },
    checkEmbedMapLocation (boundingRect, target) {
      const entryPos = boundingRect.height - boundingRect.top
      if (entryPos > 0 && boundingRect.top < 200 && boundingRect.top > 0) {
        const post = this.$refs.embedsRef.find(e => e.$el.dataset.refid === target.dataset.refid)
        this.currentActiveState = { state: post.postData.state, location: post.postData.location }
        this.$emit('onActiveState', this.currentActiveState)
      }
    },
    onLoadEmbed ({ provider, el, entry }) {
      switch (provider) {
        case 'Instagram': {
          if (this.instgrm) { this.instgrm.Embeds.process() }
          break
        }
        case 'TikTok': {
          // console.log(this.tiktokEmbed)
          if (this.tiktokEmbed) { this.tiktokEmbed.lib.render([el]) }

          break
        }
        case 'Twitter': {
          if (this.twttr) { this.twttr.widgets.load(el) }
          break
        }
      }
    },
    filteredEmbeds (category) {
      return this.embedsData.embeds.filter(e => e.categories.includes(category.name))
    },
    setCategory (category) {
      this.selectedCategory = category
      this.$emit('onSelectCategory', this.selectedCategory)
      this.$refs.line.scrollIntoView()
    },
    async getScripts () {
      if (process.client) {
        this.twttr = await d3require.require('https://platform.twitter.com/widgets.js').catch(
          () => window.twttr)
        this.instgrm = await d3require.require('https://instagram.com/embed.js').catch(
          () => window.instgrm
        )
        this.tiktokEmbed = await new Promise((resolve) => {
          d3require.require('https://www.tiktok.com/embed.js').catch(
            () => setTimeout(() => resolve(window.tiktokEmbed), 1000)
          )
        })
      }
    }
  }
}
</script>

<style lang="scss" scoped>
@import "~@/css/vars";

.tab-link {
  font-family: $baseFont;
  position: relative;
  border: none;
  outline: none;
  cursor: pointer;
  padding-left: 1rem;
  padding-right: 1rem;
  padding-top: 0.2rem;
  font-size: 0.8rem;
  border-top-left-radius: 10px;
  -webkit-clip-path: polygon(
    0 0,
    0 100%,
    100% 100%,
    100% calc(100% - 10px),
    calc(100% - 10px) 0
  );
  clip-path: polygon(
    0 0,
    0 100%,
    100% 100%,
    100% calc(100% - 10px),
    calc(100% - 10px) 0
  );
}
.tab-header::before {
  position: absolute;
  content: "";
  width: 100%;
  height: 100%;
  top: 0px;
  margin-top: -0.5rem;
  background-color: white;
}
.tab-header {
  position: relative;
  background-color: white;
  padding-top: 1.15rem;
  margin-bottom: -0.5rem;
  z-index: 1000;
}
.embeds-container {
  padding-top: 1rem;
  padding-bottom: 1rem;
}
.sticky {
  position: sticky;
  top: 68px;
}
</style>
