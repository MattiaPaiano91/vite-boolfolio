<script>
import AppHeader from "./components/AppHeader.vue";
import AppFooter from "./components/AppFooter.vue";
import AppMain from "./components/AppMain.vue";
import { data } from "./store.js";

export default {
  data() {
    return {
      data,
    };
  },
  components: {
    AppHeader,
    AppMain,
    AppFooter,
  },
  methods: {},
  mounted() {
  },
};
</script>

<template>
  <AppHeader />
  <div :class="data.themeFlag ? 'mode-light' : 'mode-dark'" class="main">
    <AppMain />
  </div>
  <AppFooter :class="data.themeFlag ? 'mode-light' : 'mode-dark'" />
</template>

<style lang="scss">
@use "assets/scss/main" as *;
@import "assets/scss/partials/reset";
</style>
