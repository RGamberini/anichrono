<template>
  <Transition name="slide-up" mode="out-in">
    <div class="full" v-if="screen === 0">
      <WelcomeScreen @next="screen++"></WelcomeScreen>
    </div>
    <div class="full" v-else><AnimeScreen></AnimeScreen></div>
  </Transition>
</template>
<script setup lang="ts">
import WelcomeScreen from './components/WelcomeScreen.vue'
import AnimeScreen from './components/AnimeScreen.vue'
import { ref } from 'vue'

const screen = ref(0)
</script>
<style scoped>
.slide-up-enter-active,
.slide-up-leave-active {
  transition: all 0.25s ease-out;
}

.slide-up-enter-from {
  opacity: 0;
  transform: translateY(30px);
}

.slide-up-leave-to {
  opacity: 0;
  transform: translateY(-30px);
}
</style>
