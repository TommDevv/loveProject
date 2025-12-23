<script setup lang="ts">
  import { ref } from 'vue'
  import StarrySkyBackground from './components/starry-sky.vue'
  const showConstLines = ref(false);

</script>

<template>
  <div>
      <StarrySkyBackground :showConstellation="showConstLines">
      <h1 class="title-container twinkle-star-regular">
        <span class="blur">Titulo Provisional</span>
        <span class="text">Titulo Provisional</span>
      </h1>
    </StarrySkyBackground>

    <div class="ground"></div>
  </div>
</template>

<style>

  .scene-container{
    position:relative;
    min-height: 200vh;
    width: 100%;
  }

  .spacer{
    height: 100vh;
  }

  .ground{
    position: sticky;
    bottom: 0;
    height:600px;
    width: 100vw;
    margin-left: calc(-50vw + 50%);
    display: block;
    background-image: url('./assets/ground/vecteezy_graphics-design-grass-on-white-background-vector_8071361-Photoroom.png');
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center bottom;
    z-index: 10;
    object-fit: cover;
  }

    html, body {
    margin: 0;
    padding: 0;
    overflow-x: hidden;

  }

  .title-container {
    position: relative;
    text-align: center;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    padding-top:20px;
  }

  .title-container span{
    position:absolute;
  }

  .blur{
    filter: blur(6px);
    opacity: 0.8;
    color:rgb(230, 144, 241)
  }

  .text {
    position: relative;
  }

</style>
