<template>
  <div class="card">
    <h1>{{ animal.name }}</h1>
    <hr />
    <img :src="`/assets/img/${animal.type}.jpg`" />
    <p>
      {{ animal.type }} (<span class="latin">{{ animal.latin }}</span
      >)
    </p>
    <p></p>
    <p>{{ animal.since }}</p>
    <p>{{ returnDiet(animal.diet) }}</p>
  </div>
</template>

<script setup lang="ts">
type Animal = {
  name: string
  type: string
  latin: string
  since: number
  diet: []
}

const animal = defineProps<Animal>()
const food = [
  'rice',
  'wheat',
  'corn',
  'meat',
  'dogfood',
  'catfood',
  'lettuce',
  'vegetables',
  'peel of vegetables and fruits'
]

function returnDiet(arr: []): string {
  let myFood = ''
  arr.forEach((item) => {
    myFood += ` ${food[item]}`
  })
  return myFood
}
</script>

<style scoped>
.card {
  width: 30vw;
  padding: 15px;
  border: grey 1px solid;
  border-radius: 5px;
  box-shadow: 3px 3px 3px rgba(0, 0, 0, 0.3);
  margin: 20px;
}
.card img {
  width: 64px;
  aspect-ratio: 1/1;
  float: left;
  margin: 10px;
}
.latin {
  font-style: italic;
}
</style>
