<script>
import AppHeader from './components/AppHeader.vue';
import AppFooter from './components/AppFooter.vue';
import { RouterView } from 'vue-router';

export default {
    data() {
        return {

        };
    },
    components: {
        AppHeader,
        AppFooter
    },  
    methods: {

    }
}
</script>

<template>

    <AppHeader />
    <router-view></router-view>
    <AppFooter />
    
</template>

<style lang="scss">
    @use "assets/scss/main" as *;
    @import "assets/scss/partials/reset";
</style>
