<template>
  <div id="app">
      <!-- header -->
      <app-header/>

      <!-- main -->
      <main>
          <main-grid/>
      </main>
  </div>
</template>

<script>
import AppHeader from './components/AppHeader.vue' 
import MainGrid from './components/MainGrid.vue'

export default {
  name: 'App',
  components: {
    AppHeader,
    MainGrid
  }
}
</script>

<style lang="scss">
@import './assets/style/general.scss';
@import './assets/style/vars.scss';

main{
  padding: $section-pad;
}

</style>
