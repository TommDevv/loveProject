<script setup lang="ts">
  import { ref } from 'vue'
</script>

<template>
  <p>HOLA MUNDO</p>
</template>

<style scoped>
  .sky-layer {
    position: fixed;
    inset: 0;
    background-image: url('assets/sky/background.png');
    background-size: cover;
    background-position: center 0%;
    z-index: -10;
    pointer-events: none;
  }

  .ground-layer {
    position: relative;
    z-index: 1;
    min-height: 200vh;
    background-image: url('assets/ground/ground.png');
  }

  .chest-layer {
    width: 400px;
    margin: 0 auto;
    margin-top: 50vh;
  }

  .spacer {
  height: 100vh;
  }
</style>
