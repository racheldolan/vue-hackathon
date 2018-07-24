<template>
  <section>
  <div class="map" :id="mapName"></div>
</section>
</template>

<script>
/* global google */
export default{
  name: 'GoogleMap',
  props: ['bikeData', 'getLocationData'],
  data () {
    return {
      mapName: this.name + '-map'
    }
  },
  mounted () {
    const element = document.getElementById(this.mapName)
    const options = {
      zoom: 13,
      center: new google.maps.LatLng(51.501527, -0.1921837)
    }
    const map = new google.maps.Map(element, options)

    this.infoWindow = new google.maps.InfoWindow()

    const trafficLayer = new google.maps.TrafficLayer()
    trafficLayer.setMap(map)

    this.bikeData.forEach((data) => {
      const position = new google.maps.LatLng(data.lat, data.lon)
      const marker = new google.maps.Marker({
        position,
        map,
        title: data.commonName
      })

      marker.addListener('click', () => {
        // map.setZoom(15)
        this.getLocationData(data.id)
      })
    })
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
