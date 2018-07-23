<template>
  <section>
    <GoogleMap v-bind:bikeData="bikeData" name="example"></GoogleMap>
    <ul>
      <li v-for="(bike, index) in bikeData" v-bind:key="index">
        {{bike.commonName}} | <strong> {{bike.lat}}, {{bike.lon}} </strong>
      </li>
    </ul>

  </section>
</template>

<script>
import axios from 'axios'
import GoogleMap from './GoogleMap'

export default {
  name: 'HelloWorld',
  data () {
    return {
      // msg: 'yo',
      bikeData: [],
      markerCoordinates: [{
        latitude: 51.501527,
        longitude: -0.1921837
      }, {
        latitude: 51.505874,
        longitude: -0.1838486
      }]
    }
  },
  mounted () {
    axios({
      method: 'GET',
      url: 'https://api.tfl.gov.uk/bikepoint'
    })
      .then(res => {
        console.log(res.data);
        this.bikeData = res.data;
      })
      .catch(err => console.log(err))
  },
  components: {
    GoogleMap
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
