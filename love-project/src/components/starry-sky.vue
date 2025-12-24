<template>
    <div class="starry-wrapper">
        <!-- fondo del cielo -->
        <div class="sky"></div>

        <!-- estrellas -->
         <div class="stars stars-1" :style="starsFastStyle"></div>
         <div class="stars stars-2" :style="starsSlowStyle"></div>

         <!-- contenido principal -->
          <div class="content" :style="contentStyle">
            <slot></slot>
          </div>

          <div class="constellation-wrapper" :style="constWrapperStyle">
                        <!-- Constelacion lineas -->
            <svg class="constellation-links" viewBox="0 0 100 100" preserveAspectRatio="none" v-if="props.showConstellation">
                <line
                    v-for="(link, index) in constellationLinks"
                    :key="index"
                    :x1="getPoint(link[0])?.x || 0"
                    :y1="getPoint(link[0])?.y || 0"
                    :x2="getPoint(link[1])?.x || 0"
                    :y2="getPoint(link[1])?.y || 0"
                    vector-effect="non-scaling-stroke"
                    pathLength="1"
                />
            </svg>
                      <!-- constelacion estrellas-->
            <div 
                v-for="point in constellationPoints"
                :key="point.id"
                class="constellation-button"
                :style="{
                    left: point.x + '%',
                    top: point.y + '%'
                }"
                @click="emitToggleModal(point.id)"
             ></div>
          </div>
    </div>
</template>

<script setup lang="ts">
    import { onBeforeUnmount, onMounted, ref, computed } from 'vue';

    defineOptions({
        name: 'StarrySkyBackground'
    });
    
    const props = defineProps<{
        showConstellation?: boolean;
    }>();

    const emit = defineEmits<{
        (e: 'open-modal', id: number): void;
        (e: 'parallax-scroll', value: number): void;
    }>();

    const scrollY = ref<number>(0);
    //listener para cuando el uruario haga scroll
    const onScroll = () => {
        scrollY.value = window.scrollY;
        emit('parallax-scroll', scrollY.value);
    };

    //modificadores del scroll para efectuar estilo "parallax"
    const starsSlowStyle = computed(() => ({
        transform: `translateY(${-scrollY.value * 0.1}px)`
    }));

    const starsFastStyle = computed(() => ({
        transform: `translateY(${-scrollY.value * 0.18}px)`
    }));

    const contentStyle = computed(() => ({
        transform: `translateY(${scrollY.value * 0.25}px)`
    }));

    const constWrapperStyle = computed(() => ({
        transform: `translateY(${-scrollY.value * 0.2}px)`
    }));

    onMounted(() => {
        window.addEventListener('scroll', onScroll, {passive: true});
    });

    onBeforeUnmount(() => {
        window.removeEventListener('scroll', onScroll);
    });

    function getPoint(id:number | undefined): {id:number, x:number, y:number} | undefined {
        return constellationPoints.value.find(p => p.id === id); 
    }

    function emitToggleModal(id:number){
        emit('open-modal', id);
    }

    //Referencia de posicion de los puntos de las constelaciones
    const constellationPoints = ref<Array<{id:number, x:number, y:number}>>([
        {id:1, x:37, y:22},
        {id:2, x:50, y:30},
        {id:3, x:63, y:22},
        {id:4, x:67, y:40},
        {id:5, x:33, y:40},
        {id:6, x:50, y:70},
    ]);

    //referencia de los puntos de conexion entre las lineas SVG de la constelacion
    const constellationLinks = [
        [2,3],
        [3,4],
        [4,6],
        [6,5],
        [5,1],
        [1,2]
    ];

</script>

<style>
    /* contenedor principal */
    .starry-wrapper {
        position: relative;
        width: 100vw;
        min-height: 70vh;
    }

    /*Fondo del cielo*/
    
    .sky {
        position: fixed;
        inset: 0;
        background: radial-gradient(
            ellipse at bottom,
                #0d2242 0%,
                #0e0111 70%,
                #000000 100%
        );
        z-index: -1;
        will-change: transform;
    }

    /* Estrellas */
    .stars {
        position: fixed;
        inset: 0;
        background-repeat: repeat;
        pointer-events: none;
        will-change: transform, opacity;
    }

    .stars-1 {
        z-index:2;
        background-image:
        radial-gradient(1.2px 2px at 20% 30%, white, transparent),
        radial-gradient(1.2px 2px at 60% 40%, white, transparent),
        radial-gradient(1.2px 2px at 50% 70%, white, transparent),
        radial-gradient(1.2px 2px at 10% 80%, white, transparent),
        radial-gradient(1.2px 2px at 70% 80%, white, transparent);
        background-size: 220px 220px;
        animation: twinkleSlow 3s infinite alternate;
    }

    .stars-2 {
        z-index: 3;
        background-image:
        radial-gradient(1.2px 2px at 30% 20%, white, transparent),
        radial-gradient(1.2px 2px at 80% 80%, white, transparent),
        radial-gradient(1.2px 2px at 70% 50%, white, transparent),
        radial-gradient(1.2px 2px at 90% 30%, white, transparent),
        radial-gradient(1.2px 2px at 10% 60%, white, transparent),
        radial-gradient(1.2px 2px at 50% 80%, white, transparent);
        background-size: 150px 150px;
        animation: twinkleFast 1.5s infinite alternate;

    }

    /*constelacion - botones*/
    .constellation-wrapper {
        position: fixed;
        inset: 0;
        z-index: 7;
        margin-top: 10vh;
        display: flex;
        align-items: center;
        justify-content: center;
        pointer-events: none;
    }

    .constellation-button {
        position:absolute;
        width: 12px;
        height: 12px;
        border-radius: 50%;
        transform: translate(-50%, -50%);
        background-image: radial-gradient(10px 10px at center, white, rgb(134, 58, 131) 40%, transparent 60%);
        animation: twinkleConstellation 2s infinite alternate;
        pointer-events: auto;
    }

    .constellation-button:hover {
        cursor: pointer;
        box-shadow: 0 0 8px 4px rgb(134, 58, 131);
        background-image: radial-gradient(10px 10px at center, white, rgb(134, 58, 131) 40%);
    }

    /*Constelacion - lineas*/

    .constellation-links {
        position: absolute;
        inset: 0;
        width: 100%;
        height: 100%;
        pointer-events: none;
    }

    .constellation-links line {
        stroke: rgba(168, 86, 223, 0.4);
        stroke-width: 1;
        stroke-linecap: round;
        filter: blur(0.1px);
        stroke-dasharray: 100;
        stroke-dashoffset: 100;
        animation: drawLine 20s ease forwards;
    }
    
    /* animaciones */
    @keyframes twinkleSlow{
        from {opacity: 0.4;}
        to {opacity: 1;}
    }

    @keyframes twinkleFast{
        from{opacity:0.2}
        to{opacity:0.9}
    }

    @keyframes twinkleConstellation{
        from{opacity:0.7}
        to{opacity:1}
    }

    @keyframes drawLine {
        to {
            stroke-dashoffset: 0;
        }
    }


    /*contenido principal */
    .content {
        position: relative;
        z-index: 5;
        height: 100%;
    }

    html, body {
    margin: 0;
    padding: 0;
    overflow-x: hidden;
    }



</style>