<template>
  <div id="app">
      <!-- header -->
      <app-header @enterTitle="giveText" />

      <!-- main -->
      <main>
          <main-grid :writtenText="writtenText"/>
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
    writtenText: ''
  }},
  methods:{
    giveText(text){
      console.log('arrivato! ', text)
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
