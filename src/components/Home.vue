<template>
  <section class="container">
    <h1 class="title">Bike Checkr App</h1>
    <div class="columns">
      <div class="column is-two-thirds-desktop">
        <GoogleMap :bikeData="bikeData" :getLocationData="getLocationData" name="example"></GoogleMap>
      </div>
      <div class="column is-one-third-desktop">
        <div class="info-box content" v-if="locationData.bikesCount >-1">
          <h1 class="title">{{locationData.name}}</h1>
          <ul>
            <li>Available bikes: {{locationData.bikesCount}}</li>
            <li>Available docks: {{locationData.emptyDocks}}</li>
          </ul>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import axios from 'axios'
import GoogleMap from './GoogleMap'

export default {
  name: 'Home',
  data () {
    return {
      locationData: {},
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
  methods: {
    getLocationData: function (bikeId) {
      console.log(bikeId)
      axios({
        method: 'GET',
        url: `https://api-radon.tfl.gov.uk/Occupancy/BikePoints/${bikeId}`
      })
        .then(res => {
          console.log(res.data[0])
          this.locationData = res.data[0]
        })
        .catch(err => console.log(err))
    }
  },
  mounted () {
    axios({
      method: 'GET',
      url: 'https://api.tfl.gov.uk/bikepoint'
    })
      .then(res => {
        console.log(res.data)
        this.bikeData = res.data
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

.info-box {
  /* width: 200px; */
  height: 200px;
  border: 1px solid red;
}
</style>
