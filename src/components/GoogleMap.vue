<template>
  <div class="map" :id="mapName"></div>
</template>

<script>
/* global google */
export default{
  name: 'GoogleMap',
  props: ['bikeData'],
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

    this.bikeData.forEach((data) => {
      const position = new google.maps.LatLng(data.lat, data.lon)
      const marker = new google.maps.Marker({
        position,
        map,
        title: data.commonName
      })

      // marker.addListener('click', function () {
      //   map.setZoom(15)
      //   // marker.title = 'Another name'
      // })
    })
  }
}
</script>

<style scoped>
.map {
  width: 800px;
  height: 600px;
  margin: 0 auto;
  background: gray;
}
</style>
