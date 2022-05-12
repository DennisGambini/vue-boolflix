<template>
  <div id="app">
      <!-- header -->
      <app-header @enterTitle="giveText" />

      <!-- main -->
      <main>
          <!-- landing -->
          <!-- :writtenText="myDefault" -->
          <main-grid 
          v-if="writtenText ==='' " 
          :myDefault="defaultSearch"
          :writtenText="defaultSearch"
          :movies="'I film più ricercati'" 
          :series="'Le serie più viste'"
          :previewNumber="5"
          />
          <!-- ricerca utente -->
          <main-grid 
          v-else 
          :writtenText="writtenText"
          :movies="'Film trovati'" 
          :series="'Serie TV trovate'"
          :previewNumber="10"
          />
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
  },
  data(){return{
    writtenText: '',
    defaultSearch: 'harry'
  }},
  methods:{
    giveText(text){
      this.writtenText = text;
    }
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
