<template>
  <footer>
      
      <input type="search" name="flag-search" id="flag-search" v-model="flagTxt" @keyup.enter="getFlags">
      <button @click="getFlags">bandiere</button>

        <div v-if="flagSrc !== undefined" class="img-box">
            <img :src="'https://countryflagsapi.com/png/' + flagSrc" :alt="flagSrc + ' flag'"/>
        </div>

  </footer>
</template>

<script>

export default {
    name: 'AppFooter',
    data(){
        return{
            flagSrc: undefined,
            flagTxt: ''
        }

    },
    methods:{
        getFlags(){
            this.flagTxt === 'en' ? this.flagSrc = 'gb' : this.flagSrc = this.flagTxt;
        }
    },
}
</script>

<style lang="scss" scoped>
@import '../assets/style/vars.scss';
    // img{
    //     height: $flag-size;
    //     width: calc($flag-size * 1.5);
    // }
</style>