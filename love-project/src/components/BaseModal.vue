<template>
    <transition name="overlay-fade">
        <div
            v-if="open"
            class="modal-overlay"
            @click.self="emitClose"
        >
            <transition name="modal-slide">
                <div class="modal-container">
                    <button class="modal-close" @click="emitClose">×</button>
                    <div class="modal-content">
                        <slot></slot>
                    </div>
                </div>
            </transition>
        </div>
    </transition>
</template>

<script setup lang="ts">
    defineOptions({
        name: 'BaseModal'
    });

    defineProps<{
        open: boolean;
    }>();

    const emit = defineEmits<{
        (e: 'close'): void;
    }>();

    const emitClose = () => {
        emit('close');
    }

</script>

<style scoped>
    .modal-overlay {
        position: fixed;
        inset:0;
        background: rgba(0, 0, 0, 0.65);
        z-index: 1000;

        display: flex;
        align-items: center;
        justify-content: center;
    }

    .modal-container {
        position:relative;
        max-width: 700px;
        width: 90%;
        max-height: 85vh;
        background:
        radial-gradient(
            ellipse at center,
            rgb(230, 206, 142) 0%,
            rgb(138, 112, 55) 80%,
            rgb(51, 41, 20) 100%

        );

        border-radius: 10px;
        padding: 2rem;
        color: rgb(46, 32, 7);
        overflow-y: auto;
        overflow-x:hidden;
        box-shadow: 0 20px 60px rgba(0, 0, 0, 0.6);
    }

    .modal-close {
        position: absolute;
        top:1rem;
        right:1rem;

        background: transparent;
        border: none;
        font-size: 1.5rem;
        cursor: pointer;
        color:black;
    }

    .modal-content {
        position: relative;
    }

    .overlay-fade-enter-active,
    .overlay-fade-leave-active {
    transition: opacity 0.3s ease;
    }

    .overlay-fade-enter-from,
    .overlay-fade-leave-to {
    opacity: 0;
    }

    .modal-slide-enter-active,
    .modal-slide-leave-active {
    transition: all 0.35s ease;
    }

    .modal-slide-enter-from {
    opacity: 0;
    transform: translateY(30px);
    }

    .modal-slide-leave-to {
    opacity: 0;
    transform: translateY(30px);
    }
</style>