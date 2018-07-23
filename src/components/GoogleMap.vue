<template>
  <div class="map" :id="mapName"></div>
</template>

<script>
export default{
  name: 'GoogleMap',
  props: [],
  data() {
    return {
      mapName: this.name + "-map",
    }
  },
  mounted() {
    const element = document.getElementById(this.mapName)
    const options = {
      zoom: 14,
      center: new google.maps.LatLng(51.501527,-0.1921837)
    }
    const map = new google.maps.Map(element, options);
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
