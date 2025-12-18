<template>
    <div class="starry-wrapper">
        <div class="sky"></div>

        <!-- estrellas -->
         <div class="stars stars-1"></div>
         <div class="stars stars-1"></div>

         <!-- contenido principal -->
          <div class="content">
            <slot></slot>
          </div>
    </div>
</template>

<script setup lang="ts">
    defineOptions({
        name: 'StarrySkyBackground'
    })
</script>

<style scooped>
    /* contenedor principal */
    .starry-wrapper {
        position: relative;
        pointer-events: none;
        overflow:hidden;
        width: 100vw;
        height: 100vh;
    }

    /*Fondo del cielo*/
    
    .sky {
        position: fixed;
        inset: 0;
        background: radial-gradient(
            ellipse at bottom,
                #0b1d3a 0%,
                #020111 70%,
                #000000 100%
        );
        z-index: -1;
    }
</style>