<template>
  <div class="plant-detail">

    <div class="plant-container">
      <div class="plant-text">
      <h2>{{ plant.name }}</h2>

      <h3>Watering Schedule</h3>

      <p>{{ plant.description }}</p>
      <p>You should water this plant <b>{{ plant.wateringSchedule }}.</b></p>

      <label>Have you watered this plant?</label>
      <input type="checkbox" v-model="userSetWatered" v-on:change="waterUpdate">
    </div>

    <div class="plant-image">   
      <img v-bind:src="photoPath(plant.photo)">
    </div> 

  </div>

  <hr>

  </div>
</template>

<script>
export default {
  name: 'HousePlant',
  emits: ['water-update'],
  props: {
    plant: Object,
    watered: Boolean
  },
  data() {
    return {
      userSetWatered: this.watered,
    }
  },
  methods: {
    waterUpdate() {
      this.$emit('water-update', this.plant.id, this.userSetWatered)
    },
    photoPath(imageFile) {
      return require('@/assets/' + imageFile)
    }
  }

}
</script>

<style scoped>

.plant-container {
  /* Flexbox - display text and image on one line, and wrap as needed
  https://css-tricks.com/snippets/css/a-guide-to-flexbox/ */
  display: flex;
  justify-content: space-evenly;
  align-content: stretch;
  flex-wrap: wrap;
}

.plant-text {
  flex-grow: 2;   /** take up twice as much space as the plant-image */
}

.plant-image {
  flex-grow: 1;
}

</style>
