<template>
  <div>
    <USAMap
      :map-data="mapData"
      :map-ready="mapReady"
      :active-state="activeState "
    />
    <div class="city">
      {{ activeState? activeState.location : '' }}
    </div>
  </div>
</template>

<script>
import USAMap from './USAMap.vue'

export default {
  name: 'MapContainer',
  components: {
    USAMap
  },
  props: {
    activeState: {
      type: Object,
      default: null,
      required: false
    }
  },
  data () {
    return {
      mapData: {},
      loadingMap: false,
      loadingData: false,
      mapReady: false
    }
  },
  computed: {

  },
  created () {
    // this.loadContentData()
    // this.loadMapData()
    // this.loadMarkersData()

  },
  mounted () {
    this.initMap()
  },
  methods: {
    async initMap () {
      await this.loadMapData()
      this.mapReady = true
    },
    async loadMapData () {
      this.loadingMap = true
      this.mapData = await fetch('maps/us-all-states-20m-ligth-basic.json')
        .then(res => res.json())
      this.loadingMap = false
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@import "~@/css/_vars";
@import "~@/css/mixins";

.margin {
  margin-left: -1.5rem;
  margin-right: -1.5rem;
}
.city {
  max-width: 75%;
  margin-left: auto;
  margin-right: auto;
  @include breakpoint(medium) {
    background-color: $grey;
  }
  font-weight: bold;
  padding: 0.2rem;
  text-align: center;
  border-radius: 0.5rem;
}
</style>
