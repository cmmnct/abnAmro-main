<template>
    <div>
        <p>This is {{ myText.name }} component</p>
        <div v-html="myText.content" class="colorpatch"></div>
        <p v-bind="customer">Mr. Hansen</p>
        <img :src="`assets/${customer['data-id']}.jpg`">
    </div>

    <div class="patch-editor">
        <input type="range" min="0" max="255" v-model="currentPatch.r">{{ currentPatch.r }}<br>
        <input type="range" min="0" max="255" v-model="currentPatch.g">{{ currentPatch.g }}<br>
        <input type="range" min="0" max="255" v-model="currentPatch.b">{{ currentPatch.b }}<br>
        <input type="range" min="0" max="1" step="0.01" v-model="currentPatch.a">{{ currentPatch.a }}<br>
        <input type="text"  v-model="currentPatch.name">{{ currentPatch.name }}<br>
        <div class="thumb-box" :style="{backgroundColor : currentColor}"></div>
    </div>

<div v-if="patches">
    <div class="thumb" v-for="patch in patches" v-bind:key="patch.id" :style="{backgroundColor: rgba(patch)}" >{{ patch.name }} {{ `rgba(${patch.r},${patch.g},${patch.b},${patch.a},)`}}</div>
</div>
    
</template>

<script setup lang="ts">
import { ref, watchEffect, computed } from 'vue';
import type { Ref } from 'vue'

export type ColorPatch = {
    r:number,
    g:number,
    b:number,
    a:number,
    id:number,
    name:string
};

const patches: Ref<ColorPatch[] | null> = ref(null);
const currentPatch:Ref<ColorPatch> = ref({
    r : 0,
    g: 0,
    b:0,
    a:1,
    id:-1,
    name:''
});

const currentColor = computed(()=>{
    return `
    rgba(${currentPatch.value.r},
    ${currentPatch.value.g},
    ${currentPatch.value.b},
    ${currentPatch.value.a})`
})

function rgba(patch:ColorPatch){
    return `
    rgba(${patch.r},
    ${patch.g},
    ${patch.b},
    ${patch.a})`
}

watchEffect(async () => {
  // this effect will run immediately and then
  // re-run whenever currentBranch.value changes
  const url = 'https://my-json-server.typicode.com/cmmnct/patchDemo/patches';
  patches.value = await (await fetch(url)).json()
})



const myText = ref({
    name : 'ColorPatch',
    content: '<div class="colorpatch"></div>',
    type: 'customer'
});

const customer = ref ({
    class : "consumer",
    'data-id': '10538'
})


</script>

<style scoped>
.colorpatch {
    width: 128px;
    aspect-ratio: 1/1;
    background-color: aqua;
}

.customer {
    color: blueviolet;
    font-weight: bold;
}

.thumb{
    width: 64px;
    aspect-ratio: 1/1;
}

.thumb-box{
    width: 50vw;
    aspect-ratio: 3/2;
}
</style>