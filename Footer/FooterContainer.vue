<template>
  <footer>
    <RelatedPostsContainer />
    <FooterMenu />
    <FooterEmailSubscribe />
  </footer>
</template>

<script>
import FooterEmailSubscribe from './FooterEmailSubscribe'
import FooterMenu from './FooterMenu'
import RelatedPostsContainer from '~/components/RelatedPosts/RelatedPostsContainer'

export default {
  components: {
    FooterEmailSubscribe,
    FooterMenu,
    RelatedPostsContainer
  }
}
</script>

<style scoped lang="scss">
footer {
  margin-top: 1rem;
}
</style>
