<script setup>
import { MapboxMap, MapboxMarker } from "@studiometa/vue-mapbox-gl";
import "mapbox-gl/dist/mapbox-gl.css";
</script>

<script>
export default {
  data() {
    return {
      token: import.meta.env.VITE_API_MAP_KEY,
      zoom: 12
    }
  },
  props: ["center"],
}
</script>

<template>
  <MapboxMap
    style="height: 65vh"
    :access-token="token"
    map-style="mapbox://styles/mapbox/streets-v12"
    :zoom="zoom"
    :center="center"
  >
    <MapboxMarker :lng-lat="center">
      <img src="../assets/images/icon-location.svg" alt="Location logo">
    </MapboxMarker>
  </MapboxMap>
</template>

<style scoped lang="sass">
@import "../input.sass"

#map
  width: 100%
  height: 200px
</style>
