<script setup lang="ts">
  import { ref, onMounted } from 'vue'
  import StarrySkyBackground from './components/starry-sky.vue'
  import BaseModal from './components/BaseModal.vue'

  const showConstLines = ref(false)
  const showModal = ref(false)
  const modalContent = ref<number>(0)
  const mainOffset = ref<number>(0)
  const pregunta1 = ref('')
  const answer1 = ref(false)
  const pregunta2 = ref('')
  const answer2 = ref(false)
  const pregunta3 = ref('')
  const answer3 = ref(false)
  const pregunta4 = ref('')
  const answer4 = ref(false)
  const pregunta5 = ref('')
  const answer5 = ref(false)
  const pregunta6 = ref('')
  const answer6 = ref(false)

  const handleOpenModal = (id:number)=>{
    modalContent.value = id
    showModal.value = true
  }

  onMounted(() => {
        handleOpenModal(0);
    });
  
  function closeAndCheckModal(){
    showModal.value = false;
    if(answer1.value && answer2.value && answer3.value && answer4.value && answer5.value && answer6.value){
      showConstLines.value = true;
    }
  }

  function verificar(pregunta: number):void{
    switch(pregunta){
      case 1:
        if(pregunta1.value.toLocaleLowerCase().trim() === "16 de mayo de 2024"){
          answer1.value = true;
        } else {
          alert("Respuesta incorrecta. Intenta de nuevo.");
        }
        break;
      case 2:
        if(pregunta2.value.toLowerCase().trim() === "i don't want to miss a thing"){
          answer2.value = true;
        } else {
          alert("Respuesta incorrecta. Intenta de nuevo.");
        }
        break;
      case 3:
        if(pregunta3.value.toLowerCase().trim() === "mariposas amarillas"){
          answer3.value = true;
        } else {
          alert("Respuesta incorrecta. Intenta de nuevo.");
        }
        break;
      case 4:
        console.log(pregunta4.value.toLowerCase().trim());
        if(pregunta4.value.toLowerCase().trim() === "imaginate"){
          answer4.value = true;
        } else {
          alert("Respuesta incorrecta. Intenta de nuevo.");
        }
        break;
      case 5:
        if(pregunta5.value.toLowerCase().trim() === "un asadero de pollos"){
          answer5.value = true;
        } else {
          alert("Respuesta incorrecta. Intenta de nuevo.");
        }
        break;
      case 6:
        if(pregunta6.value.toLowerCase().trim() === "tumblr"){
          answer6.value = true;
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
      @open-modal="handleOpenModal"
      @parallax-scroll="value => mainOffset = value"
      >
      <h1 class="title-container twinkle-star-regular">
        <span class="blur">Mi cielito estrellado</span>
        <span class="text">Mi cielito estrellado</span>
      </h1>
    </StarrySkyBackground>

    <div class="memories-wrapper" :style="{transform: `translateY(${-mainOffset * 0.2}px)`}" v-if="showConstLines">
      <img src="./assets/memories/background1.jpg" style="top: 40px; left: 100px; animation-delay: 0s;"/>
      <img src="./assets/memories/background2.jpg" style="top: 50px; right: 100px; animation-delay: 1s;"/>
      <img src="./assets/memories/background 3.jpg" style="bottom: 130px; left: 30px; animation-delay: 2s;"/>
      <img src="./assets/memories/background 4.jpg" style="bottom: 150px; right: 70px; animation-delay: 3s;"/>
    </div>

    <div class="second-title-container" v-if="showConstLines">
      <h1 class="title-container medievalsharp-regular">
        <img src="./assets/memories/pergamino2.png" @click="handleOpenModal(7)"/>
        <span class="blur-2">You Are My Density</span>
        <span class="text">You Are My Density</span>
      </h1>
    </div>

    <BaseModal :open="showModal" @close="closeAndCheckModal">
      <!-- contenido del modal 0 -->
      <div id="content-1" v-if="modalContent==0" class="modal-content">
        <br>
        <p>
          Hoy como todos los dias celebro el lazo que tengo con la mujer que mas amo en este mundo.
          Cada momento a tu lado brilla en mi corazón como un mar de estrellas que iluminan mi camino y mi pensar.
          Quiero que redescubras junto a mi el brillo de cada momento que pasamos juntos y es tan importante para mi.
        </p>
        <br>
        <p>Toca las estrellas que destacan entre el cielo estrellado para descubrir recuerdos y una vez hayas terminado
          y completes la constelacion, bajo tierra habrá enterrado un tesoro que concebí desde el fondo de mi corazón.
        </p>
        <button class="qabutton" @click="closeAndCheckModal">Aceptar</button>
      </div>
      <!-- Pregunta del modal 1 -->
      <div id="content-1" v-if="modalContent==1 &&!answer1" class="modal-content">
        <h2 style="color:black">¿En que fecha nos dimos nuestro primer beso?</h2>
        <input class="qainput" type="text" v-model="pregunta1">
        <button class="qabutton" @click="verificar(1)">Verificar</button>
      </div>
      <!-- Respuesta del modal 1 -->
      <div id="answer-1" v-if="modalContent == 1 && answer1">
        <h2 style="color:black">Nuestro Primer Beso</h2>
        <div class="image-wrapper">
          <img src="./assets/memories/primer beso.jpg" alt="Nuestro Primer Beso" />
        </div>
        <label style="font-weight: bold; margin-bottom: 10px;">El dia que me enamore del sabor de tus labios y desde entonces no quiero dejar de besarte jamás</label>
      </div>
      <!-- Pregunta del modal 2 -->
      <div id="content-2" v-if="modalContent==2 && !answer2" class="modal-content">
        <h2 style="color:black">¿Cuál es el nombre de nuestra canción?</h2>
        <input class="qainput" type="text" v-model="pregunta2">
        <button class="qabutton" @click="verificar(2)">Verificar</button>
      </div>
      <!-- Respuesta del modal 2 -->
      <div id="answer-2" v-if="modalContent == 2 && answer2">
        <h2 style="color:black">Nuestra Canción</h2>
        <label style="font-weight: bold; margin-bottom: 10px;">No quiero perderme ni un segundo a tu lado mi amor</label>
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

      <!-- Pregunta del modal 3 -->
      <div id="content-3" v-if="modalContent==3 && !answer3" class="modal-content">
        <h2 style="color:black">¿Que animal sirve para aliviar el estrés?</h2>
        <label>Pista: Dato austiciado exclusivamente por mi</label>
        <input class="qainput" type="text" v-model="pregunta3">
        <button class="qabutton" @click="verificar(3)">Verificar</button>
      </div>
      <!-- Respuesta del modal 3 -->
      <div id="answer-3" v-if="modalContent == 3 && answer3">
        <h2 style="color:black">No solo para el estrés, tambien para recordar lo que me haces sentir</h2>
        <div class="image-wrapper">
          <img src="./assets/memories/mariposas amarillas.jpg" alt="Mariposas amarillas" />
        </div>
        <label style="font-weight: bold; margin-bottom: 10px;">
              Esa foto me hizo imaginar como nos veríamos de bonitos siendo pareja, mi amor, tu eres un sueño del que nunca quiero despertar. 
              Hoy sigo sintiendo mariposas amarillas en mi estomago cada vez que nos vemos.
        </label>
      </div>
      <!-- Pregunta del modal 4 -->
      <div id="content-4" v-if="modalContent==4 && !answer4" class="modal-content">
        <h2 style="color:black">Nombre de la cancion de Silvio Rodríguez que me dedicaste</h2>
        <label>No puedo evitar recordarte y sentir amor por ti cada vez que la escucho</label>
        <input class="qainput" type="text" v-model="pregunta4">
        <button class="qabutton" @click="verificar(4)">Verificar</button>
      </div>

      <!-- Respuesta del modal 4 -->
      <div id="answer-2" v-if="modalContent == 4 && answer4">
        <h2 style="color:black">Imaginate - Silvio rodriguez</h2>
        <label style="font-weight: bold; margin-bottom: 10px;">Las letras de silvio que siempre me hacen querer poder tenerte entre mis brazos</label>
        <div class="video-wrapper">
          <iframe
            src="https://www.youtube.com/embed/irGeiYCxtWQ"
            title="Imaginate - Silvio rodriguez"
            frameborder="0"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
            allowfullscreen
        ></iframe>
        </div>
      </div>
      <!-- Pregunta del modal 5 -->
      <div id="content-5" v-if="modalContent==5 && !answer5" class="modal-content">
        <h2 style="color:black">Que local prometimos montar juntos para cometer fraude fiscal</h2>
        <input class="qainput" type="text" v-model="pregunta5">
        <button class="qabutton" @click="verificar(5)">Verificar</button>
      </div>
      <!-- Respuesta del modal 5 -->
      <div id="answer-3" v-if="modalContent == 5 && answer5">
        <h2 style="color:black">Tu y yo todos los dias haciendo mucho mua mua así a dos cuadras del mar, piensalo</h2>
        <div class="image-wrapper">
          <img src="./assets/memories/beso-pollo.jpg" alt="Mariposas amarillas" />
        </div>
        <label style="font-weight: bold; margin-bottom: 10px;">
              Puede ser asi para siempre. ¿Si quieres? Siono
        </label>
      </div>
      <!-- Pregunta del modal 6 -->
      <div id="content-6" v-if="modalContent==6 && !answer6" class="modal-content">
        <h2 style="color:black">Uno de tus sueños de la infancia que cumplimos juntos por un día</h2>
        <label>Pista - Ser una chica:</label>
        <input class="qainput" type="text" v-model="pregunta6">
        <button class="qabutton" @click="verificar(6)">Verificar</button>
      </div>

      <!-- Respuesta del modal 6 -->
      <div id="answer-6" v-if="modalContent == 6 && answer6">
        <h2 style="color:black">Mi Chica Tumblr</h2>
        <div style="display: flex; gap: 10px; justify-content: center; align-items: center;">
          <div class="image-wrapper" style="flex: 1; max-width: 400px;">
        <img src="./assets/memories/chica-tumblr.jpg" alt="Chica Tumblr 1" />
          </div>
          <div class="image-wrapper" style="flex: 1; max-width: 400px;">
        <img src="./assets/memories/chica-tumblr2.jpg" alt="Chica Tumblr 2" />
          </div>
        </div>
        <label style="font-weight: bold; margin-bottom: 10px; display: block; font-size: 18px;">
          Cosita bonita, mujer dueña de mis ojos de mi corazón y de mis pensamientos.
          siempre tan hermosa embriagandome en tu belleza y tu ternura. Quedate conmigo para siempre.
        </label>
      </div>
      <!-- Contenido del modal 7 -->
      <div id="content-7" v-if="modalContent==7" class="modal-content" >
        <h1 class="medievalsharp-regular">Momento Infinito</h1>
        <div class="medievalsharp-regular" style="font-size: 150%; justify-content: start;">
            <p>Lejano siento el viento</p>
            <p>Emoción inunda el ambiente.</p>
            <p>Empieza el día, voy a verte</p>
            <p>Todo lo que soy se deforma y se comprime </p>
            <p>Es tu amor para mí, todo </p>
            <br>
            <p>Cerca, sólo de mí te siento</p>
            <p>Ferviente pasión en mi corazón y en mi mente</p>
            <p>Todo mi ser empieza a deshacerse</p>
            <p>Son tus brazos, me atraparon para siempre</p>
            <br>
            <p>Efímero, es el tiempo traicionero</p>
            <p>Dulzura de mi vida, es cuando estoy contigo</p>
            <p>Todo lo que soy pasa a ser tuyo</p>
            <p>Son tus ojos, me embriagaron sin aviso</p>
            <br>
            <p>Infinito es el sentimiento,</p>
            <p>La lejanía se siente cálida,</p>
            <p>la noche se hace día, la amargura se vuelve dulce,</p>
            <p>Finalmente cesa mi anhelo y el tiempo se detiene</p>
            <p>Lo poco que queda de mí se reconstruye,</p>
            <p>Efímero fue ese eterno segundo</p>
            <p>Son tus besos reformulando mi mundo.</p>
            <p>23/12/2025</p>
            <br>
            <h2>Con cariño, tu gordito.</h2>
            <h2>Te Amo.</h2>
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

  .blur-2{
    filter: blur(6px);
    opacity: 0.8;
    color:rgb(241, 231, 144)
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

    .image-wrapper {
      width: 100%;
      max-width: 520px;
      aspect-ratio: 16 / 9;
      display: flex;
      margin: 16px auto;
      align-items: center;
      justify-content: center;
      overflow: hidden;
    }

    .image-wrapper img {
      width: 100%;
      height: 100%;
      object-fit: contain;
      display: block;
    }

    .memories-wrapper {
      position: fixed;
      inset: 0;
      pointer-events: none;
      z-index: 6;
      opacity: 0;
      animation: fadeIn 2s ease forwards;
    }

    .memories-wrapper img {
      width: 200px;
      height: 200px;
      position: absolute;
      object-fit: cover;
      display: block;
      border-radius: 8px;
      opacity: 0.7;
      box-shadow: 0 0 10px 5px rgba(192, 100, 189, 0.575);
      animation: floatingImages 4s ease-in-out infinite;
    }

    .second-title-container {
      position: absolute;
      text-align: center;
      z-index: 12;
      top: 900px;
      left: 0;
      right: 0;
      margin: 0;
      padding: 0;
    }

    .second-title-container img {
      position: absolute;
      width: 100%;
      max-width: 400px;
      height: auto;
      display: block;
      margin: 0 0;
      padding: 0;
      bottom: 0.2px;
      cursor: pointer;
      transition: filter 0.3s ease;
    }

    .second-title-container img:hover {
      filter: drop-shadow(0 0 12px rgb(241, 231, 144)) drop-shadow(0 0 6px rgb(241, 231, 144));
    }

    /* Animacion de las imagenes Flotantes*/
    @keyframes floatingImages {
      0% {
        transform: translateY(0px);
      }
      50% {
        transform: translateY(-10px);
      }
      100% {
        transform: translateY(0px);
      }
    }

    @keyframes fadeIn {
      to {
        opacity: 1;
      }
    }

</style>
