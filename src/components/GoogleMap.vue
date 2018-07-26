<template>
  <div class="map"></div>
</template>

<script>
/* global google */
export default{
  name: 'GoogleMap',
  props: ['bikeData', 'getLocationData', 'bikeToggle'],
  mounted () {
    const options = {
      zoom: 12.4,
      center: new google.maps.LatLng(51.501527, -0.141099)
    }
    this.map = new google.maps.Map(this.$el, options)

    this.infoWindow = new google.maps.InfoWindow()

    const trafficLayer = new google.maps.TrafficLayer()
    trafficLayer.setMap(this.map)
  },
  watch: {
    bikeData () {
      this.bikeData.forEach((data) => {
        const position = new google.maps.LatLng(data.lat, data.lon)
        const marker = new google.maps.Marker({
          position,
          map: this.map,
          title: data.commonName
        })
        marker.addListener('click', () => {
          this.map.setZoom(15)
          this.getLocationData(data.id)
        })
      })
    }
  }
}
</script>

<style scoped>
.map {
  max-width: 800px;
  height: 600px;
  margin: 0 auto;
  background: gray;
}
</style>
