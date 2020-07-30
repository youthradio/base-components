<template>
  <div>
    <div ref="mapmap" class="map" />
  </div>
</template>

<script>
import { Runtime, Inspector } from '@observablehq/runtime'
import notebook from '3f03c8ac5dc1a903'

export default {
  props: {
    cellName: {
      type: String,
      required: true
    }
  },
  data() {
    return {}
  },
  computed: {},
  mounted() {
    const runtime = new Runtime()
    const inspect = Inspector.into(this.$refs.mapmap)
    runtime.module(notebook, (name) => {
      return (
        (name === this.cellName ||
          name === (this.cellName === 'map' ? 'viewof yearButon' : null)) &&
        inspect()
      )
    })
  },
  methods: {}
}
</script>

<style lang="scss" scoped>
@import '~@/css/mixins';
@import '~@/css/vars';
/deep/ .map {
  svg {
    font-family: 'Assistant', sans-serif !important;
    font-weight: 800;
  }
  .title {
    text-align: center;
    font-size: 1rem;
    font-weight: bold;
    font-family: 'Assistant', sans-serif !important;
    font-weight: 800;
    @include breakpoint(medium) {
      font-size: 0.7rem;
    }
  }
  .legend-title {
    font-weight: bold;
  }
  .annotation-note-title {
    font-size: 1.7rem;
    fill: $black;
    stroke: $white;
    stroke-opacity: 0.7;
    stroke-width: 1.8;
    margin: 2px;
    paint-order: stroke;
    @include breakpoint(medium) {
      font-size: 1rem;
    }
  }
  .axis {
    font-size: 1.2rem;
    font-weight: normal;
    @include breakpoint(medium) {
      font-size: 0.8rem;
    }
  }

  .annotation-note-label {
    font-size: 1.1rem;
    fill: $black;
    stroke: $white;
    stroke-opacity: 0.7;
    stroke-width: 1.8;
    margin: 2px;
    paint-order: stroke;

    @include breakpoint(medium) {
      font-size: 0.6rem;
    }
  }

  [data-mode='N/A'] {
    font-size: 1rem;
  }
  .linechart .annotation-note-label {
    font-size: 1rem;
    fill: $black;
    paint-order: stroke;
    @include breakpoint(medium) {
      font-size: 1rem;
    }
  }
  .state-label {
    text-transform: uppercase;
    font-weight: bold;
  }
  .state {
    stroke: darkgray;
    stroke-width: 1px;
    stroke-linejoin: round;
    // fill: #fdc997;
  }

  .age-legend {
    font-size: 1rem;
    text-anchor: middle;
    @include breakpoint(medium) {
      font-size: 0.7rem;
    }
  }
  .buttons {
    margin-top: 0.5rem;
  }
  button {
    position: relative;
    font-family: 'Assistant', sans-serif;
    font-size: 0.8rem;
    font-weight: bold;
    background-color: $white;
    border-color: $black;
    border-radius: 0.3rem;
    border-width: 0.05rem;
    padding-left: 0.3rem;
    padding-right: 0.3rem;
    margin: 5px;
    box-shadow: 0px 2px #0000004a;
    @include breakpoint(medium) {
      font-size: 1.1rem;
    }
  }
  button:hover {
    box-shadow: 0px 0px #0000004a;
  }
  button:active {
    background-color: $lightgrey;
    box-shadow: 0px 1px #0000004a;
  }
  button.active {
    background-color: $lightgrey;
    box-shadow: 0px 1px #0000004a;
  }
  button:focus {
    outline: none;
  }
  .linechart {
    .annotation-note-label {
      font-size: 1.1rem;
      fill: $black;
      paint-order: stroke;
      @include breakpoint(medium) {
        font-size: 0.7rem;
      }
    }
    .axis {
      font-size: 1.2rem;
      font-weight: normal;

      @include breakpoint(medium) {
        font-size: 0.8rem;
      }
    }
  }
  .click-anima {
    // z-index: 100;
    pointer-events: none;
    position: absolute;
    top: 50%;
    left: 50%;
    width: 30px;
    height: 30px;
    // margin: 100px auto;
    background-color: #333;
    border-radius: 100%;
    animation: scaleout 1s infinite ease-in-out;
  }
  @keyframes scaleout {
    0% {
      transform: translate(-15px, -15px) scale(0);
    }
    100% {
      transform: translate(-15px, -15px) scale(1.2);
      opacity: 0.2;
    }
  }
}
</style>
