<script setup lang="ts">
import { ref } from 'vue'

interface Restaurant {
  name?: string
  status?: restaurantStatus
  dishes?: Dish[]
}
type restaurantStatus = 'Want to try' | 'Recommended' | 'Do not Recomend' | 'Must Try'
const restaurantList = ref<Restaurant[]>([])
const newRestaurant = ref<Restaurant>({})

function addRestaurant() {
  restaurantList.value.push({
    name: newRestaurant.value.name,
    status: 'Want to try',
    dishes: []
  })
}
</script>

<template>
  <main>
    <pre>{{ newRestaurant }}</pre>
    <!-- create user to allow that user to add a restourant to list -->
    <form @submit.prevent="addRestaurant">
      <div>
        <label for="restaurant-name">Restaurant Name</label>
        <input id="restaurant-name" v-model="newRestaurant.name" type="text" />
      </div>
      <div>
        <label for="restaurant-status">Restaurant Status</label>
        <input id="restaurant-status" v-model="newRestaurant.status" type="text" />
      </div>
      <button type="submit">Add Restaurant</button>
    </form>
    <ul>
      <li v-for="restaurant in restaurantList" :key="restaurant.name">{{ restaurant.name }}</li>
    </ul>
  </main>
</template>
