<script setup>
import {ref, reactive} from "vue";

const score = ref(0) //score player
const moleIndex = ref(null) //position mole
const holes = reactive(new Array(9).fill(false)); //holes number
const gameOver = ref(false) //the end game

const moleTimer = ref(undefined);
const clickMarkers = ref([]);

function startGame() {
  score.value = 0;
  gameOver.value = false;
  spawnMole();

  setTimeout(() => {
    gameOver.value = true;
    clearInterval(moleTimer.value);
    moleIndex.value = null;
  }, 30000);


  function spawnMole() {
    moleIndex.value = Math.floor(Math.random() * holes.length)

    moleTimer.value = setInterval(() => {
      moleIndex.value = Math.floor(Math.random() * holes.length)
    }, 1000)
  }

}

function pingMole(index) {
  const isCorrect = index === moleIndex.value;

  if (isCorrect) {
    score.value++;
    moleIndex.value = null;
  } else {
    score.value--;
  }

  clickMarkers.value.push({
    index,
    correct: isCorrect,
  })

  setTimeout(() => {
    clickMarkers.value.shift()
  }, 1000)
}

function endGame() {
  gameOver.value = true;
  clearInterval(moleTimer.value);
  moleIndex.value = null;
}
</script>

<template>
  <div class="game min-h-screen p-5 relative bg-cover bg-center">
    <img src="./assets/bac.jpg"
         alt="background"
         class="absolute inset-0 w-full h-full object-cover z-[-1] "
    />

    <h1 class="text-4xl font-bold text-black text-center mb-2 p-2">Ping mole 🎯</h1>
    <p class="font-bold text-2xl text-center mb-2 p-2">Your score: {{ score }}</p>

    <div class="grid grid-cols-3 gap-4 mt-4 select-none	">

      <div
          v-for="(hole, index) in holes"
          :key="index"
          :class="
            [
              'hole h-25 w-25 rounded-full relative mx-auto p-12 m-6 shadow-2xl',
              {
                mole: moleIndex === index,
                'bg-red-400': clickMarkers.find(cm => cm.index === index && cm.correct === false),
                'bg-green-400': clickMarkers.find(cm => cm.index === index && cm.correct === true),
                'bg-zinc-800': !clickMarkers.find(cm => cm.index === index),
              }
            ]
          "
          @click="pingMole(index)"

      >
        <img
            v-if="moleIndex === index"
            src="./assets/mole.png"
            alt="Mole"
            class="absolute inset-0 w-full h-full object-cover cursor-pointer"/>

        <div class="absolute top-2 left-0 transform -translate-y-full">
          <img src="./assets/flower.png"
               alt="Flowers"
               class="w-12 h-12"/>
        </div>
      </div>
    </div>
    <div class="flex justify-center mt-16 space-x-4">

      <button class="btn-squash space-x-4 mx-2 relative w-48 h-16  rounded-full border-none bg-[#976fff]
    text-white shadow-[0px_10px_10px_rgba(210,187,253,1) inset,
    0px_5px_10px_rgba(5,5,5,0.212), 0px_-10px_10px_rgba(124,54,255,1) inset]
    cursor-pointer flex items-center justify-center transition-transform
    duration-300 hover:scale-105"
              @click="startGame">
        Start Game
        <span class="absolute top-1 left-1 w-[70%] h-[2px] bg-white opacity-70 blur-sm rounded-full"></span>
        <span class="absolute bottom-1 left-1 w-[70%] h-[2px] bg-white opacity-10 blur-sm rounded-full"></span>

      </button>
      <button
          class="btn-squash space-x-4 mx-2 relative w-48 h-16 rounded-full border-none bg-red-500 text-white shadow-[0px_10px_10px_rgba(210,187,253,1) inset, 0px_5px_10px_rgba(5,5,5,0.212), 0px_-10px_10px_rgba(124,54,255,1) inset] cursor-pointer flex items-center justify-center transition-transform duration-300 hover:scale-105"
          @click="endGame"

      >
        Game Over
        <span class="absolute top-1 left-1 w-[70%] h-[2px] bg-white opacity-70 blur-sm rounded-full"></span>
        <span class="absolute bottom-1 left-1 w-[70%] h-[2px] bg-white opacity-10 blur-sm rounded-full"></span>
      </button>
      <div>
        <p class="font-bold text-2xl text-center mb-4 p-3  bg-cover" v-if="gameOver">Finish Game! Your score: {{
            score
          }} 🎉</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.hole {
  position: relative;
  transition: background-color 0.3s;
}

</style>
