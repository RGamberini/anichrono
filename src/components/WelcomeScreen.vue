<template>
  <div style="height: 50vh; display: flex; flex-direction: column">
    <div class="main-image"></div>
    <h1>Anichrono</h1>
    <div class="play-button" @click="$emit('next')">Play</div>
  </div>
  <div style="height: 35vh; width: 100%"></div>
</template>
<script setup lang="ts"></script>
<style scoped>
.main-image {
  flex-grow: 1;
  background-image: url('Daco_4185534.png');
  background-position: center center;
  background-repeat: no-repeat;
  background-size: cover;
}
</style>
