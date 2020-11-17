<template>
  <div>
    <div id="map" ref="map" />
  </div>
</template>

<script>
import { geoAlbersUsaTerritories } from 'd3-composite-projections'
import * as topojson from 'topojson-client'
import d3 from '../../../util/d3'

const WIDTH = 960
const HEIGHT = 500

export default {
  name: 'USAMap',
  props: {
    contentData: {
      type: Array,
      default: null,
      required: false,
    },
    mapData: {
      type: Object,
      default: null,
      required: true,
    },
    mapReady: {
      type: Boolean,
      default: false,
      required: true,
    },
    activeState: {
      type: Object,
      default: null,
      required: false,
    },
  },
  data() {
    return {
      svg: null,
      aspect: null,
      projection: null,
      path: null,
      isMapReady: false,
    }
  },
  computed: {},
  watch: {
    mapReady() {
      if (this.mapReady) {
        this.drawMap()
        if (this.activeState) {
          this.setStateColor(this.activeState.state, this.activeState.color)
        }
      }
    },
    activeState: {
      handler(newval, oldval) {
        if (newval && !oldval) {
          this.setStateColor(newval.state, newval.color)
        } else if (newval.state !== oldval.state) {
          this.setStateColor()
          this.setStateColor(newval.state, newval.color)
        }
      },
      deep: true,
    },
  },
  created() {},
  mounted() {
    this.createSvg()
    // topojson.feature(this.mapData, this.mapData.objects.states).features
  },
  methods: {
    createSvg() {
      this.svg = d3.select(this.$refs.map).append('svg')
      this.aspect = WIDTH / HEIGHT
      this.projection = geoAlbersUsaTerritories().translate([
        WIDTH / 2,
        HEIGHT / 2,
      ])
      this.path = d3.geoPath(this.projection)
      // this.svg.attr('width', WIDTH)
      //   .attr('height', HEIGHT)
      this.svg.attr('viewBox', '0 0 ' + WIDTH + ' ' + HEIGHT)
      // .attr('perserveAspectRatio', 'xMinYMid meet')
      this.svg.style('width', '100%').style('height', 'auto')
      const defs = this.svg.append('defs')
      // create filter with id #drop-shadow
      // height=130% so that the shadow is not clipped
      const filter = defs
        .append('filter')
        .attr('id', 'drop-shadow')
        .attr('height', '130%')

      // SourceAlpha refers to opacity of graphic that this filter will be applied to
      // convolve that with a Gaussian with standard deviation 3 and store result
      // in blur
      filter
        .append('feGaussianBlur')
        .attr('in', 'SourceAlpha')
        .attr('stdDeviation', 5)
        .attr('result', 'blur')
      // translate output of Gaussian blur to the right and downwards with 2px
      // store result in offsetBlur
      filter
        .append('feOffset')
        .attr('in', 'blur')
        .attr('dx', 5)
        .attr('dy', 5)
        .attr('result', 'offsetBlur')
      // overlay original SourceGraphic over translated blurred opacity by using
      // feMerge filter. Order of specifying inputs is important!
      const feMerge = filter.append('feMerge')
      feMerge.append('feMergeNode').attr('in', 'offsetBlur')
      feMerge.append('feMergeNode').attr('in', 'SourceGraphic')
      this.resizeContainer()
      window.addEventListener('resize', this.resizeContainer)
    },
    getTransform(el) {
      const transform = d3.select(el).style('transform')
      const g = document.createElementNS('http://www.w3.org/2000/svg', 'g')
      g.setAttributeNS(null, 'transform', transform)
      const value = g.transform.baseVal.consolidate()
      if (!value) {
        return { x: 0, y: 0 }
      }
      return { x: value.matrix.e, y: value.matrix.f }
    },
    drawMap() {
      this.svg
        .append('g')
        .attr('class', 'boundaries')
        .append('path')
        // .attr('filter', 'url(#drop-shadow)')
        .attr(
          'd',
          this.path(
            topojson.mesh(
              this.mapData,
              this.mapData.objects.states,
              (a, b) => a === b
            )
          )
        )

      this.svg
        .append('g')
        .selectAll('.states')
        .data(
          topojson.feature(this.mapData, this.mapData.objects.states).features
        )
        .enter()
        .append('path')
        .attr('class', 'states')
        .attr('d', this.path)
        .attr('fill', 'gray')

      // this.svg.append('path')
      //   .style('fill', 'none')
      //   // .style('stroke', 'black')
      //   .attr('d', this.projection.getCompositionBorders())
    },
    setStateColor(state = null, color = 'gray') {
      this.svg
        .selectAll('.states')
        .filter((e) => (!state ? true : state === e.properties.STUSPS))
        .attr('fill', color)
    },
    resizeContainer() {
      const targetWidth = parseInt(this.svg.node().parentNode.clientWidth)
      this.svg.attr('width', targetWidth)
      this.svg.attr('height', Math.round(targetWidth / this.aspect))
    },
    // setAnimation (state) {
    //   if (state && !this.timer) {
    //     this.timer = setInterval(() => {
    //       this.yearSlider = (this.yearSlider + 1) % this.yearsButtonsData.length
    //     }, 600)
    //   } else {
    //     clearInterval(this.timer)
    //   }
    // }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@import '~@/css/vars';
@import '~@/css/mixins';

/deep/ #map {
  .state-label {
    text-transform: uppercase;
    font-weight: bold;
  }
  .states {
    stroke: darkgray;
    stroke-width: 1px;
    stroke-linejoin: round;
    // fill: #fdc997;
  }
  .state-borders {
    fill: none;
    stroke: $dark;
    stroke-width: 3px;
    stroke-linejoin: round;
    stroke-linecap: round;
    pointer-events: none;
  }
}
</style>
