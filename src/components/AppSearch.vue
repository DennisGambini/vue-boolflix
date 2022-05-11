<template>
  <div>
      <input type="search" name="app-search" id="app-search" placeholder="..." v-model="movieText" @keyup.enter="$emit('enterTitle', movieText)">
      <button @click="$emit('enterTitle', movieText)">Cerca</button>
      <!-- <i class="fa-solid fa-heart"></i> -->
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
    height: 30px;
    padding-left: 20px;
    color: white;
    background-color: $bg-body;
    // text-transform: uppercase;
}
button{
    margin-left: 10px;
    background-color: $bg-body;
    color: white;
    border: 1px solid;
    border-radius: 5px;
    padding: 5px;
    cursor: pointer;
    text-transform: uppercase;
}


</style>