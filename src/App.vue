<template>
  <div id="app">
      <!-- header -->
      <app-header @enterTitle="giveText" class="header" @langChange="giveLang" />
      <!-- main -->
      <main>
          <div class="last-research" v-if="writtenText">
            <span>ultima ricerca effettuata:</span>
            <span>{{lastResearch}}</span>
          </div>

          <!-- landing -->
          <main-grid 
          v-if="writtenText ==='' " 
          :myDefault="defaultSearch"
          :writtenText="defaultSearch"
          :movies="'I film più amati'" 
          :series="'Le serie TV più viste'"
          :previewNumber="5"
          @lastResearch="setLastResearch"
          />
          <!-- ricerca utente -->
          <main-grid 
          v-else 
          :writtenText="writtenText"
          :movies="'Film trovati per  ' + lastResearch" 
          :series="'Serie TV trovate per  ' + lastResearch"
          :previewNumber="10" 
          :languageSelected="language" 
          @lastResearch="setLastResearch"
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
    defaultSearch: 'harry',
    language: '',
    lastResearch: ''
  }},
  methods:{
    giveText(text){
      this.writtenText = text;
      this.$emit('textChange', this.writtenText)
    },
    giveLang(lang){
      this.language = lang;
      this.$emit('langChange', this.language)
    },
    setLastResearch(value){
      this.lastResearch = `"${value}"`
    },
  }
}
</script>

<style lang="scss">
@import './assets/style/general.scss';
@import './assets/style/vars.scss';

.header{
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 2;
}
main{
  margin-top: 81px;
  padding: $section-pad;
  .last-research{
    font-size: 0.9rem;
    color: $text-color;
    span:first-of-type{
      margin-right: 20px;
    }
    span:last-of-type{
      font-size: 1.2em;
    }
  }
}

</style>
