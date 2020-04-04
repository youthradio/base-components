<template>
  <div>
    <slot />
  </div>
</template>

<script>
import Plyr from 'plyr'

export default {
  name: 'VuePlyr',
  props: {
    /** Options object for plyr config. **/
    options: {
      type: Object,
      required: false,
      default () {
        return {}
      }
    },
    /** Array of events to emit from the plyr object **/
    emit: {
      type: Array,
      required: false,
      default () { return [] }
    }
  },
  data () {
    return {
      player: {}
    }
  },
  computed: {
    opts () {
      const options = this.options
      if (!{}.hasOwnProperty.call(this.options, 'hideYouTubeDOMError')) {
        options.hideYouTubeDOMError = true
      }
      return options
    }
  },
  mounted () {
    this.player = new Plyr(this.$el.firstChild, this.opts)
    this.emit.forEach((element) => {
      this.player.on(element, this.emitPlayerEvent)
    })
  },
  beforeDestroy () {
    try {
      this.player.destroy()
    } catch (e) {
      if (!(this.opts.hideYouTubeDOMError && e.message === 'The YouTube player is not attached to the DOM.')) {
        // eslint-disable-next-line no-console
        console.error(e)
      }
    }
  },
  methods: {
    emitPlayerEvent (event) {
      this.$emit(event.type, event)
    }
  }
}
</script>

<style lang="scss">
@import "~@/node_modules/plyr/dist/plyr.css";
@import "~@/css/vars";

.plyr--full-ui input[type=range] {
  // -webkit-appearance: none;
  // background: 0 0;
  // border: 0;
  // border-radius: 26px;
  color: $green;
  // display: block;
  // height: 19px;
  // margin: 0;
  // padding: 0;
  // transition: box-shadow .3s ease;
  // width: 100%;
}

.plyr--audio .plyr__control.plyr__tab-focus,
.plyr--audio,
.plyr--video,
.plyr--audio .plyr__control:hover,
.plyr--audio .plyr__control[aria-expanded=true],
.plyr--video .plyr__control:hover,
.plyr--video .plyr__control[aria-expanded=true],
.plyr__control--overlaid
{
  background: $green;
}
</style>
