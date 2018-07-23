<template>
  <div class="map" :id="mapName"></div>
</template>

<script>
export default{
  name: 'GoogleMap',
  props: ['bikeData'],
  data() {
    return {
      mapName: this.name + "-map",
    }
  },
  mounted() {
    const element = document.getElementById(this.mapName)
    const options = {
      zoom: 13,
      center: new google.maps.LatLng(51.501527,-0.1921837)
    }
    const map = new google.maps.Map(element, options);

    this.bikeData.forEach((coord) => {
      const position = new google.maps.LatLng(coord.lat, coord.lon);
      const marker = new google.maps.Marker({
        position,
        map
      });
    });
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
