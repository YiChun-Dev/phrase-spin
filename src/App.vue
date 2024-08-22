<script setup lang="ts">
import { PhraseSpin } from '.'

const phrases: string[] = [
  "Hello, World !",
  "Welcome to PhraseSpin",
  "Vue.js is awesome !",
  "TypeScript makes it even better !"
]

const handleAnimationComplete: () => void = () => console.log('Animation complete')
</script>

<template>
  <div class="App">

    <header>
      <h1>PhraseSpin Demo</h1>
    </header>

    <main>
      <PhraseSpin :phrases="phrases" :animation="'bounceIn'" :speed="2000" :complete="handleAnimationComplete" />
    </main>

    <footer>
      <p>&copy; 2024 PhraseSpin. All rights reserved.</p>
    </footer>

  </div>
</template>

<style scoped>
.App {
  display: flex;
  flex-direction: column;
  min-height: 100vh
}

header,
footer {
  background-color: #282c34;
  color: white;
  padding: 20px;
  text-align: center
}

main {
  flex: 1 0 auto;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
  font-size: 18px
}
</style>