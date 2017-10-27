<template>
  <div id="app">
    <button style="position: absolute; top: 15px; left: 15px; z-index: 99999;" v-on:click="addAttribution">Add Attribution</button>

    <v-mapboxgl
      :id="mapId"
      :access-token="mapAccessToken"
      :height="mapHeight"
      :width="mapWidth"
      :gl-center="mapCenter"
      :gl-controls="mapControls"
      :gl-zoom="mapZoom"
      :gl-style="mapStyle"
      :gl-bearing="mapBearing"
      :gl-pitch="mapPitch">
    </v-mapboxgl>
  </div>
</template>

<script>
import credentials from '../credentials.json'
console.log('credentials:', credentials)
export default {
  data ()  {
    return {
      mapId: 'map',
      mapAccessToken: credentials.apiKey,
      mapHeight: window.innerHeight,
      mapWidth: window.innerWidth,
      mapCenter: {
        autodiscover: true
      },
      mapControls: {
        navigation: {
          enabled: true,
          options: {}
        }
      },
      mapZoom: {
        value: 8
      },
      mapStyle: 'mapbox://styles/abgordon/ciqk5q6q4000qbkm12cmqgbuf',
      mapBearing: {
        value: 40
      },
      mapPitch: {
        value: 60
      }
    }
  },
  methods: {
    handleResize (event) {
      this.mapHeight = event.currentTarget.innerHeight
      this.mapWidth = event.currentTarget.innerWidth
    },
    addAttribution (event) {
      this.mapControls = Object.assign({}, this.mapControls, { attribution: { enabled: true }});
    }
  },
  mounted () {
    window.addEventListener('resize', this.handleResize)

    this.$on('mapboxglMap:styleChanged', function (event, args) {
      console.log(event, args);
    });
  }
}
</script>

<style>
body {
  margin: 0;
}
</style>
