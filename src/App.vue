<script setup lang="ts">
import { onMounted, type Ref, ref } from 'vue';

const ballPosition: Ref<{top: number, left: number}> = ref({left: 100, top: 600});
const ballDirection: Ref<{top: number, left: number}> = ref({left: 1, top: -1});

const amountRows: Ref<number> = ref(5);

const blocksPerOddRow: Ref<number> = ref(9);
const displayWidth = window.innerWidth;
const displayHeight = window.innerHeight;



const gameLoop: number = setInterval(() => {
  ballPosition.value.top += ballDirection.value.top;
  ballPosition.value.left += ballDirection.value.left;
}, 10)

let blocks: HTMLCollectionOf<Element>;
onMounted(() => {
  blocks = document.getElementsByClassName('block');
  
});


function mouseClickPosition(event: MouseEvent) {
  console.log('top:', event.clientY);
  console.log('left:', event.clientX);
}
</script>

<template>
  <div @click="mouseClickPosition">
    <div v-for="rowIndex in [...Array(amountRows).keys()]" class="d-flex" :style="`margin: 0 ${rowIndex%2!=0 ? (displayWidth/blocksPerOddRow)/2 : 0}px`">
      <div :style="`width: ${displayWidth/blocksPerOddRow}px;`" v-for="block in Array(rowIndex%2==0 ? blocksPerOddRow : blocksPerOddRow-1)" :class="`bc-${rowIndex} m-1 border block`"></div>
    </div>
  </div>
  <div id="ball" class="bg-primary position-absolute ball" :style="`top: ${ballPosition.top}px; left: ${ballPosition.left}px`"></div>
  <div class="w-100 slider-wrapper position-absolute bottom-0">
    <div class="py-2 px-5 slider h-100 bg-info-subtle"></div>
  </div>
</template>

<style scoped>
.ball {
  height: 3vh;
  border-radius: 50%;
  aspect-ratio: 1/1;
}
.block {
  height: 4vh;
  /* width: 10vw; */
}

.bc-1 {
  background-color: #FFB997;
}
.bc-2 {
  background-color: #F67E7D;
}
.bc-3 {
  background-color: #843B62;
}
.bc-4 {
  background-color: #0B032D;
}
.bc-0 {
  background-color: #74546A;
}
</style>
