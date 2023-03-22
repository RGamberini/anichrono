<template>
  <div style="height: 85vh; display: flex; flex-direction: column">
    <div class="main-image" :style="{ 'background-image': `url(${anime.images[0]})` }"></div>
    <div style="width: 50vw; height: 50px"></div>
  </div>
  <div style="width: 50%; margin-bottom: 64px" id="values-slider"></div>
  <div v-if="points === -1" class="play-button" @click="setPoints()">Submit</div>
  <h2 v-if="points > -1">{{ anime.title }}</h2>
  <h2 v-if="points > -1">{{ anime.subtitle }}</h2>
  <h2 v-if="points > -1">Points: {{ points }}</h2>
  <div v-if="points > -1" class="play-button" style="margin-bottom: 64px" @click="nextImage()">
    Next
  </div>
</template>
<script setup lang="ts">
import { ref } from 'vue'
import noUiSlider from 'nouislider'
import { PipsMode } from 'nouislider'
import 'nouislider/dist/nouislider.css'
import { onMounted } from 'vue'
import _animes from '../assets/animes.json'
const animes = _animes.filter((anime) => anime.subtitle.includes('TV-Series'))
const points = ref(-1)
const anime = ref(animes[Math.floor(Math.random() * animes.length)])
onMounted(() => {
  var slider = document.getElementById('values-slider')
  if (slider !== null) {
    noUiSlider.create(slider, {
      start: [1997],
      range: {
        min: 1997,
        max: 2023
      },
      step: 1,
      tooltips: true,
      format: { from: (num: any) => num, to: (num: any) => Math.trunc(num) },
      pips: {
        mode: PipsMode.Steps
      }
    })
  }
})

function setPoints() {
  var slider = document.querySelector('.noUi-tooltip')
  if (slider === null || slider.textContent === null) return
  let guessYear = parseInt(slider.textContent)
  let animeYear = parseInt(anime.value.subtitle.split('(')[1].split(')')[0])
  console.log(animeYear)
  console.log(1000 - Math.abs((guessYear - animeYear) * 100))
  points.value = Math.max(1000 - Math.abs((guessYear - animeYear) * 100), 0)
}
function nextImage() {
  anime.value = animes[Math.floor(Math.random() * animes.length)]
  points.value = -1
}
</script>
<style scoped>
.main-image {
  flex-grow: 1;
  background-image: url('https://cdn.anisearch.com/images/anime/screen/18/18249/full/496935.webp');
  background-position: center center;
  background-repeat: no-repeat;
  background-size: cover;
}
</style>
