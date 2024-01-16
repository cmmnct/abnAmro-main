<template>
    <div>
<h1>{{props.animal.name}}</h1>
    </div>
</template>

<script setup lang="ts">
import Animal from './zooList.vue'
const props = defineProps({
  animal: { type: Animal, required: true }
})



</script>

<style scoped>

</style>