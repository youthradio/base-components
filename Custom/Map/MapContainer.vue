<template>
  <div>
    <div class="margin">
      <USAMap
        :map-data="mapData"
        :content-data="contentData"
        :map-ready="mapReady"
      />
    </div>
    <div class="city">
      Oakland, California
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
    this.initMap()
  },
  mounted () {
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
.margin {
  margin-left: -1.5rem;
  margin-right: -1.5rem;
}
.city{
  background-color: $grey;
  font-weight: bold;
  padding: 0.2rem;
  text-align: center;
  border-radius: 0.5rem;
}
</style>
