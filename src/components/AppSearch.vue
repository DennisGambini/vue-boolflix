<template>
  <div class="container">

      <div>
        <input type="search" name="app-search" id="app-search" placeholder="Cerca un titolo..." v-model="movieText" @keyup.enter="$emit('enterTitle', movieText); reset()">
        <button @click="$emit('enterTitle', movieText); reset()">
            <i class="fa-solid fa-magnifying-glass"></i>
        </button>
      </div>
      
      <div>
        <label for="lang">
            <i class="fa-solid fa-globe"></i>
        </label>
        <select name="lang" id="lang" v-model="languageSelected" @change="$emit('langChange', languageSelected)">
            <option v-for="(item, index) in languages" :key="index" :value="item">{{item}}</option>
        </select>
      </div>
  </div>
</template>

<script>
export default {
    name: 'AppSearch',
    data(){return{
        movieText: '',
        languageSelected: '',
        languages:['it', 'en', 'es', 'br', 'jp', 'de', 'dk', 'fr' ]
    }},
    methods:{
        reset(){
            this.movieText = ''
        }
    }
}
</script>

<style lang="scss" scoped>
@import '../assets/style/vars.scss';

.container{
    @include flex-row-between-center;
    gap: 30px;
}

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
label[for="lang"]{
    color: $title-color;
    margin-right: 5px;
}


</style>