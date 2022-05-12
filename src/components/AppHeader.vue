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
            this.myMovie = text;
            console.log(this.myMovie)
            this.$emit('enterTitle', this.myMovie)
        }
    }
}
</script>

<style lang="scss" scoped>
@import '../assets/style/vars.scss';

    header{
        padding: $section-pad;
        background-color: $bg-header;
        background: linear-gradient($bg-header 30%, $bg-body 90%);
        @include flex-row-between-center;
        h1{
            color: red;
            text-transform: uppercase;
           
        }
    }
</style>