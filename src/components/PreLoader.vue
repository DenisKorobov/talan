<template>
    <transition-group name="preloader" tag="div">
        <div class="preloader-circle" :key="1"></div>
        <div class="preloader-background" :key="2"></div>
    </transition-group>
</template>

<style lang="scss" scoped>
@import '../assets/variables.scss';

.preloader-circle {
    width: 80px;
    height: 80px;
    border: 10px solid $green;
    border-right-color: transparent;
    border-radius: 50%;
    animation: preloader-rotate 1s linear infinite;
    position: fixed;
    top: 50%;
    left: 50%;
    margin-top: -40px;
    margin-left: -40px;
    z-index: 3;
}

.preloader-background {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.6);
    z-index: 2;
}

@keyframes preloader-rotate {

    0% {
        transform: rotate(0);
    }

    100% {
        transform: rotate(360deg);
    }

}
</style>
