<template>
  <section>
    <h1>yo</h1>
    <ul>
      <li v-for="bike in bikeData">
        {{bike.commonName}} | <strong> {{bike.lat}}, {{bike.lon}} </strong>
      </li>
    </ul>

  </section>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HelloWorld',
  data () {
  return {
      msg: 'yo',
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
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
