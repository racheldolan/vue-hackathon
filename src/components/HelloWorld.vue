<template>
  <section>
    <GoogleMap name="example"></GoogleMap>
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
      bikeData: []
    }
  },
  mounted () {
    axios({
      method: 'GET',
      url: 'https://api.tfl.gov.uk/bikepoint'
    })
      .then(res => this.bikeData = res.data)
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
