<template>
  
  <h1>Houseplant Water Tracker</h1>

  <watering-summary
    v-bind:summary="wateringSummary" />

  <plant-detail v-for="plant in plants" 
    v-bind:key="plant.id"
    v-bind:plant="plant"
    v-on:water-update="wateringUpdate" />

</template>

<script>
import PlantDetail from './components/HousePlant.vue'
import WateringSummary from './components/WateringSummary.vue'

export default {
  name: 'App',
  components: {
    PlantDetail,
    WateringSummary
  },
  data() {
    return {
      plants: [
        { 
          id: 1,
          name: 'Elephant Ear Plant',
          description: 'Fast growing plant with decorative leaves.',
          wateringSchedule: 'weekly',
          photo: 'elephant_ear.jpeg'
        },
        { 
          id: 2,
          name: 'Snake Plant',
          description: 'Hardy houseplant with minimal water requirements.',
          wateringSchedule: 'monthly',
          photo: 'snake_plant.jpeg'
        },
        { 
          id: 3,
          name: 'Swiss Cheese Plant',
          description: 'Large houseplant with distinctive perforated leaves.',
          wateringSchedule: 'weekly',
          photo: 'swiss_cheese.jpeg'
        },

      ],
      wateringSummary: []
    }
  },
  mounted() {
    this.plants.forEach( plant => {
      this.wateringSummary.push( {id: plant.id, name: plant.name, watered: false } )
    })
  },
  methods: {
    wateringUpdate(id, wasWatered) {
      // find plant with this id, and update entry in wateringSummary
      let updatedPlant = this.wateringSummary.find( plant => plant.id == id)
      if (updatedPlant) {
        updatedPlant.watered = wasWatered
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
