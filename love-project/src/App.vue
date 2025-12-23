<script setup lang="ts">
  import { ref } from 'vue'
  import StarrySkyBackground from './components/starry-sky.vue'
  import BaseModal from './components/BaseModal.vue';

  const showConstLines = ref(false);
  const showModal = ref(false);
  const modalContent = ref<number>(0);
  const pregunta2 = ref<string>('');
  const answer2 = ref<boolean>(false);

  function verificar(pregunta: number):void{
    switch(pregunta){
      case 2:
        if(pregunta2.value.toLowerCase().trim() === "i don't want to miss a thing"){
          answer2.value = true;
        } else {
          alert("Respuesta incorrecta. Intenta de nuevo.");
        }
        break;
      default:
        break;
    }
  }

</script>

<template>
  <div>
      <StarrySkyBackground 
      :showConstellation="showConstLines"
      @toggle-modal-1="modalContent = 1; showModal = !showModal"
      @toggle-modal-2="modalContent = 2; showModal = !showModal"
      >
      <h1 class="title-container twinkle-star-regular">
        <span class="blur">Titulo Provisional</span>
        <span class="text">Titulo Provisional</span>
      </h1>
      <button @click="showConstLines = !showConstLines">Prender constelaciones</button>
      <button @click="showModal = !showModal">Abrir Modal</button>
    </StarrySkyBackground>

    <BaseModal :open="showModal" @close="showModal = false">
      <!-- Pregunta del modal 2 -->
      <div id="content-2" v-if="modalContent==2 && !answer2" class="modal-content">
        <h2 style="color:black">¿Cuál es el nombre de nuestra canción?</h2>
        <input class="qainput" type="text" v-model="pregunta2">
        <button class="qabutton" @click="verificar(2)">Verificar</button>
      </div>
      <!-- Respuesta del modal 2 -->
      <div id="answer-2" v-if="modalContent == 2 && answer2">
        <h2 style="color:black">Nuestra Canción</h2>
        <div class="video-wrapper">
          <iframe
            src="https://www.youtube.com/embed/JkK8g6FMEXE"
            title="I Don't Want to Miss a Thing - Aerosmith"
            frameborder="0"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
            allowfullscreen
        ></iframe>
        </div>
      </div>
    </BaseModal>

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

      .video-wrapper {
        position: relative;
        width: 100%;
        aspect-ratio: 16/9;
    }

    .video-wrapper iframe {
        position: absolute;
        inset: 0;
        width: 100%;
        height: 100%;
        border: none;
    }

    .qainput{
      display: block;
      margin: 10px;
      justify-content: center;
      justify-self: center;
      font-size: medium;
      background-color: transparent;
      border-bottom: 3px solid black;
      outline: none;
      border-top: none;
      border-left: none;
      border-right: none;
      color: black;
      font-weight: bold;
      text-align: center;
    }

    .modal-content{
      text-align: center;
      justify-content: center;
    }

</style>
