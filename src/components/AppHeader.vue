<template>
  <header>
        <h1>boolflix</h1>
        <app-search @enterTitle="setTitle" @langChange="langChange"/>
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
        myMovie:'',
        dioboia: ''
    }},
    methods:{
        setTitle(text){
            console.log(text)
            this.myMovie = text;
            this.$emit('enterTitle', this.myMovie)
        },
        langChange(e){
            this.$emit('langChange', e)
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
            color: $title-color;
            text-transform: uppercase;
           
        }
    }
</style>