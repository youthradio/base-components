<template>
  <div
    v-if="isEnable"
    class="overlay"
  >
    <div class="close">
      <a
        href=""
        @click.prevent="toggle"
      >
        <svg
          aria-hidden="true"
          focusable="false"
          data-prefix="far"
          data-icon="times-circle"
          role="img"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 512 512"
          class="close-icon"
        >
          <path
            fill="currentColor"
            d="M256 8C119 8 8 119 8 256s111 248 248 248 248-111 248-248S393 8 256 8zm0 448c-110.5 0-200-89.5-200-200S145.5 56 256 56s200 89.5 200 200-89.5 200-200 200zm101.8-262.2L295.6 256l62.2 62.2c4.7 4.7 4.7 12.3 0 17l-22.6 22.6c-4.7 4.7-12.3 4.7-17 0L256 295.6l-62.2 62.2c-4.7 4.7-12.3 4.7-17 0l-22.6-22.6c-4.7-4.7-4.7-12.3 0-17l62.2-62.2-62.2-62.2c-4.7-4.7-4.7-12.3 0-17l22.6-22.6c4.7-4.7 12.3-4.7 17 0l62.2 62.2 62.2-62.2c4.7-4.7 12.3-4.7 17 0l22.6 22.6c4.7 4.7 4.7 12.3 0 17z"
          /></svg>
      </a>
    </div>
    <CustomFormat :topic="topic" />
  </div>
</template>

<script>
import CustomFormat from './CustomFormat'

export default {
  components: {
    CustomFormat
  },
  props: {
    topic: {
      type: Object,
      default: null
    }
  },
  data () {
    return {
      isEnable: false
    }
  },
  watch: {
    topic () {
      this.isEnable = true
    }
  },
  mounted () {
    window.addEventListener('keydown', (e) => {
      if (e.keyCode === 27 || e.keyCode === 32) { this.setState(false) }
    })
  },
  methods: {
    toggle () {
      this.isEnable = !this.isEnable
    },
    setState (state) {
      this.isEnable = state
    }
  }
}
</script>

<style lang="scss" scoped>
.overlay {
  z-index: 100;
  position: fixed;
  height: 100%;
  width: 100%;
  background-color: rgba(gray, 1);
  top: 0px;
  left: 0px;
  overflow-y: scroll;
}
.close-icon {
  width: 50px;
  height: auto;
  color: white;
  stroke: rgba(#333333, 0.6);
  stroke-width: 10px;
}
a,
a:hover {
  text-decoration: none;
  color: unset;
  border-bottom: unset;
  background-color: unset;
}
.close {
  z-index: 200;
  position: fixed;
  top: 0px;
  right: 0px;
}
</style>
