<template>
    <div id="app">
        <nav class="nav">
            <router-link to="/">Домашняя</router-link>
            <router-link to="/users">Пользователи</router-link>
        </nav>
        <router-view @change-preloader="preloader = $event"></router-view>
        <PreLoader v-show="preloader" />
    </div>
</template>

<script lang="ts">
import Vue from 'vue'
import PreLoader from '@/components/PreLoader.vue'

export default Vue.extend({
    name: 'App',
    components: {
        PreLoader
    },
    data() {
        return {
            preloader: false
        }
    },
})
</script>

<style lang="scss">
@import './assets/variables.scss';

* {
    box-sizing: border-box;
}

ul {
    margin: 0;
    padding: 0;
}

li {
    list-style: none;
}

#app {
    margin-top: 30px;
    font-family: Arial, Helvetica, sans-serif;
    font-size: 16px;

    .nav a {
        padding: 15px;
        color: $green-transparent;
        font-weight: bold;
        text-decoration: none;
    }

    .nav .router-link-exact-active {
        color: $green;
    }

    .main {
        padding: 0 15px;
    }
}
</style>
