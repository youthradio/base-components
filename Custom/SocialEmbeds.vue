<template>
  <div class="container">
    <div class="tab-header">
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
    <div
      v-for="category in embedsData.categories"
      :key="category.name"
      :style="[{backgroundColor:selectedCategory.color},selectedCategory.name !== category.name ? ({display: 'none'}):null]"
    >
      <Embed
        v-for="post in filteredEmbeds(category)"
        :key="post.user"
        :post-data="post"
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
      type: Array,
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
  },
  mounted () {

  },
  methods: {
    filteredEmbeds (category) {
      return this.embedsData.embeds.filter(e => e.categories.includes(category.name))
    },
    setCategory (category) {
      this.selectedCategory = category
    },
    async getScripts () {
      this.twttr = await d3require.require('https://platform.twitter.com/widgets.js').catch(
        () => window.twttr)
      this.instgrm = await d3require.require('https://instagram.com/embed.js').catch(
        () => window.instgrm
      )
      this.tiktokEmbed = await new Promise((resolve) => {
        d3require.require('https://www.tiktok.com/embed.js').catch(
          () => setTimeout(() => resolve(window.tiktokEmbed), 500)
        )
      })
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
  font-size: 1rem;
  border-top-left-radius: 10px;
  -webkit-clip-path: polygon(0 0, 0 100%, 100% 100%, 100% 40%, 85% 0);
  clip-path: polygon(0 0, 0 100%, 100% 100%, 100% 40%, 85% 0);
}
.tab-header {
  padding-top: 1.15rem;
}
</style>
