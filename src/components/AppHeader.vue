<template>
  <header>
        <h1>boolflix</h1>
        <app-search @enterTitle="setTitle" />
  </header>
</template>

<script>
import AppSearch from './AppSearch.vue'
export default {
    name: 'AppHeader',
    components: { 
        AppSearch 
    },
    data(){return{
        myMovie:''
    }},
    methods:{
        setTitle(text){
            //console.log(text)
            this.myMovie = text;
            console.log(this.myMovie)
            this.$emit('enterTitle', this.myMovie)
        }
        // emitto(){
            
        // }
    }
}
</script>

<style lang="scss" scoped>
@import '../assets/style/vars.scss';

    header{
        padding: $section-pad;
        @include flex-row-between;
        h1{
            color: red;
            text-transform: uppercase;
           
        }
    }
</style>