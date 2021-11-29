<template>
  
  <div>

    <h2>Summary</h2>

    <h4>You have watered these plants</h4>

    <div v-if="watered.length">
        <p v-for="plant in watered" v-bind:key="plant.id">
            {{ plant.name }} has been watered {{ plant.wateringSchedule }}
        </p>
        </div>
    <div v-else class="empty-list-message">
        <p>No plants have been watered.</p>
    </div>


    <h4>You have NOT watered these plants</h4>

    <div v-if="notWatered.length"> 
        <p v-for="plant in notWatered" v-bind:key="plant.id">
            {{ plant.name }} needs to be watered {{ plant.wateringSchedule }}
        </p>
    </div>
    <div v-else class="empty-list-message">
        <p>All plants have been watered.</p>
    </div>

  </div>

</template>

<script>
export default {
  name: 'WateringSummary',
  props: {
      summary: Array
  },
  computed: {
      watered() {
        let wateredPlants = [] 
          this.summary.forEach( plant => {
              if (plant.watered) {
                  wateredPlants.push(plant)
              }
          })
          return wateredPlants
          // Or, the one-liner version with filter,
          // return this.summary.filter( plant => plant.watered)
      },
      notWatered() {
          return this.summary.filter( plant => !plant.watered)
      }
  }
    
}
</script>

<style>

.empty-list-message {
    font-style: italic;
}

</style>
