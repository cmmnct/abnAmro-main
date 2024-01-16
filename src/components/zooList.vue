<template>
  <div>
    <h1>Zoo list added</h1>
    <table>
      <tr>
        <th>name</th>
        <th>type</th>
        <th>latin name</th>
        <th>since</th>
        <th>diet</th>
      </tr>
      <tbody v-if="animals">
        <tr v-for="(animal, index) in animals" :key="index">
          <td>{{ animal.name }}</td>
          <td>{{ animal.type }}</td>
          <td>{{ animal.latin }}</td>
          <td>{{ animal.since }}</td>
          <td>{{ animal.diet }}</td>
        </tr>
      </tbody>
      <tbody v-else>
        <tr>
          <td colspan="5">Loading....</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup lang="ts">
import { ref, watchEffect } from 'vue'
import type { Ref } from 'vue'

type Animal = {
  name: string
  type: string
  latin: string
  since: number
  diet: []
}

const animals: Ref<Animal[] | null> = ref(null)

watchEffect(async () => {
  // this effect will run immediately and then
  // re-run whenever currentBranch.value changes
  const url = 'assets/animals.json'
  animals.value = await (await fetch(url)).json()
})
</script>

<style scoped></style>
