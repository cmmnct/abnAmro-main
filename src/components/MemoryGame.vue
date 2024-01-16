<template>
    <div id="game-container">
        <div v-if="cards" class="field">
            <div v-for="(card, index) in cards" :key="index" class="card" @click="onClickCard($event, card)">
                <img :src="`assets/img/${card.card1}.jpg`">
                <div class="cover"></div>
            </div>
        </div>


    </div>
</template>

<script setup lang="ts">
import { ref, watchEffect } from 'vue';
import type { Ref } from 'vue'

type Card = {
    set: string,
    card1: string,
    card2:string
}
let card1: HTMLDivElement;
let card2: HTMLDivElement;


const cards: Ref<Card[] | null> = ref(null);

watchEffect(async () => {
  // this effect will run immediately and then
  // re-run whenever currentBranch.value changes
  const url = 'https://my-json-server.typicode.com/cmmnct/cards/cards';
    cards.value = shuffle(await (await fetch(url)).json());

})

/* function onClickCard(evt:Event) {
    let trgt = evt.target as HTMLImageElement;
    console.log(trgt.src);
} */
 
function onClickCard(evt:MouseEvent, card:Card) {
    console.log(card.card1);
    card1 = evt.target as HTMLDivElement;
    console.log(card1);

    card1.className = '';

}

function shuffle(array: Array<Card>): Card[] {
    array = array.concat(array);
  var m = array.length, t, i;
  // While there remain elements to shuffle…
  while (m) {
    // Pick a remaining element…
    i = Math.floor(Math.random() * m--);

    // And swap it with the current element.
    t = array[m];
    array[m] = array[i];
    array[i] = t;
  }
  return array;
}


</script>

<style lang="css" scoped>

.field {
    display: flex;
    flex-wrap: wrap;
    width: 50vw;
}
.card {
margin: 5px;
width: calc( 16.6666% - 10px);
position: relative;
}
.card img {
    max-width: 100%;
    aspect-ratio: 1/1;
}

.cover{
    width: 100%;
    aspect-ratio: 1/1;
    position: absolute;
    top: 0;
    left: 0;
    background-color: brown;
}

</style>