<template>
  <div>
      <input type="search" name="app-search" id="app-search" v-model="movieText" @keyup.enter="$emit('enterTitle', movieText)">
  </div>
</template>

<script>
export default {
    name: 'AppSearch',
    data(){return{
        movieText: ''
    }},
    methods:{
        
    }
}
</script>

<style lang="scss" scoped>
@import '../assets/style/vars.scss';

input{
    width: 200px;
    height: 100%;
}


</style>