<template>
  <div>
    <div
      ref="mapmap"
      class="map"
    />
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
  data () {
    return {
    }
  },
  computed: {

  },
  mounted () {
    const runtime = new Runtime()
    const inspect = Inspector.into(this.$refs.mapmap)
    runtime.module(notebook, (name) => {
      return (name === this.cellName || name === (this.cellName === 'map' ? 'viewof yearButon' : null)) && inspect()
    })
  },
  methods: {

  }
}
</script>

<style lang="scss" scoped>
@import "~@/css/mixins";

svg {
  font-family: "Assistant", sans-serif !important;
  font-weight: 800;
}

/deep/ .map {
  --black: #333;
  --white: #fff;
  --grey: grey;
  --lightgrey: lightgrey;

  .title {
    text-align: center;
    font-size: 1rem;
    font-weight: bold;
    font-family: "Assistant", sans-serif !important;
    font-weight: 800;
    @include breakpoint(medium) {
      font-size: 0.7rem;
    }
  }
  .legend-title {
    font-weight: bold;
  }
  .annotation-note-title {
    font-size: 1.5rem;
    fill: var(--black);
    stroke: var(--white);
    stroke-opacity: 0.7;
    stroke-width: 1.8;
    margin: 2px;
    paint-order: stroke;
    @include breakpoint(medium) {
      font-size: 1.5rem;
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
    font-size: 1rem;
    fill: var(--black);
    stroke: var(--white);
    stroke-opacity: 0.7;
    stroke-width: 1.8;
    margin: 2px;
    paint-order: stroke;

    @include breakpoint(medium) {
      font-size: 0.8rem;
    }
  }

  [data-mode="N/A"] {
    font-size: 1rem;
  }
  .linechart .annotation-note-label {
    font-size: 1rem;
    fill: var(--black);
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
  button {
    font-family: "Assistant", sans-serif;
    font-size: 1.1rem;
    font-weight: bold;
    background-color: var(--white);
    border-color: var(--black);
    border-radius: 0.3rem;
    padding-left: 0.3rem;
    padding-right: 0.3rem;
    margin: 5px;
    box-shadow: 0px 2px #0000004a;
  }
  button:hover {
    box-shadow: 0px 0px #0000004a;
  }
  button:active {
    background-color: var(--lightgrey);
    box-shadow: 0px 1px #0000004a;
  }
  button.active {
    background-color: var(--lightgrey);
    box-shadow: 0px 1px #0000004a;
    @include breakpoint(medium) {
      font-size: 1.2rem;
    }
  }
  button:focus {
    outline: none;
  }
}
</style>
