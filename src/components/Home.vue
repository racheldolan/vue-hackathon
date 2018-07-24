<template>
  <section class="container">
    <h1 class="title is-1">Bike Checkr App</h1>
    <hr />
    <h5 class="title is-5">Filter for available bikes only? <span @click="filterAvailableBikes">Yes</span></h5>
    <div class="columns">
      <div class="column is-two-thirds-desktop">
        <GoogleMap :bikeData="bikeData" :getLocationData="getLocationData" name="example"></GoogleMap>
      </div>
      <div class="column is-one-third-desktop">
        <div class="info-box content">
          <p class="subtitle" v-if="!locationData.name">Click a marker for location-specific information.</p>
          <div v-if="locationData.bikesCount >-1">
            <h1 class="title">{{locationData.name}}</h1>
            <ul>
              <li>Available bikes: {{locationData.bikesCount}}</li>
              <li>Available docks: {{locationData.emptyDocks}}</li>
            </ul>
          </div>
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
      markerCoordinates: []
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
  height: 200px;
}

span {
  cursor: pointer;
  background-color: orange;
  color: white;
  padding: 5px 10px;
  border-radius: 10%;
}

</style>
