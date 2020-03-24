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
        selectedCategory.name !== category.name ? ({display: 'none'}):null
      ]"
    >
      <Embed
        v-for="(post,id) in filteredEmbeds(category)"
        :key="post.user"
        ref="embedsRef"
        :data-refid="id"
        :post-data="post"
        @onLoadEmbed="onLoadEmbed"
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
      tiktokEmbed: null
    }
  },
  computed: {
  },
  created () {
    this.getScripts()
    this.selectedCategory = this.embedsData.categories[0]
    this.$emit('onSelectCategory', this.selectedCategory)
  },
  mounted () {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.boundingClientRect.y < 20) {
          // console.log(entry.target.dataset)
          const post = this.$refs.embedsRef[entry.target.dataset.refid]
          this.$emit('onActiveState', { state: post.postData.state, location: post.postData.location })
        }
      })
    },
    {
      threshold: Array(100).fill().map((_, i) => i / 100)
    })
    this.$refs.embedsRef.map(e => observer.observe(e.$el))
  },
  methods: {
    onLoadEmbed ({ provider, el }) {
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
.tab-link {
  position: relative;
  border: none;
  outline: none;
  cursor: pointer;
  padding-left: 0.5rem;
  padding-right: 0.5rem;
  font-size: 0.8rem;
  border-top-left-radius: 10px;
  -webkit-clip-path: polygon(0 0, 0 100%, 100% 100%, 100% calc(100% - 10px), calc(100% - 10px) 0);
  clip-path: polygon(0 0, 0 100%, 100% 100%, 100% calc(100% - 10px), calc(100% - 10px) 0);
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
