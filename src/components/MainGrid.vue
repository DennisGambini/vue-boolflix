<template>
  <section>

    <div v-if="writtenText" class="wrapper">
        <app-card  v-for="(card, index) in cards" :key="index" class="card" :card="card" :imgUrl="imgUrl"/>
    </div>
      
  </section>
</template>

<script>
import axios from 'axios'
import AppCard from './AppCard.vue';

export default {
  components: { AppCard },

    name: 'MainGrid',
    props:{
        writtenText: String
    },
    data(){
        return{
            //movie: {},
            apiUrl: 'https://api.themoviedb.org/3',
            imgUrl:'https://image.tmdb.org/t/p',
            myApiKey: '2ef36b734d4be91dd7af56b7d0142468',
            myQuery: '',
            cards:[]
        }
    },
    methods:{
        callApi(){
            if(this.myQuery !== this.writtenText){
                this.myQuery = this.writtenText;
                axios.get(`${this.apiUrl}/search/movie/?api_key=${this.myApiKey}&query=${this.myQuery}&language=it-IT`)
                .then((res) => {
                //console.log(res.data.results[0]);
                //this.movie = {...res.data.results[0]};
                console.log(res.data.results)
                this.cards = [...res.data.results]
                })
                .catch((err) => {
                console.log(err);
                })
            }
            
        }
        
    },
    updated(){
        this.callApi()
    },
}
</script>

<style lang="scss" scoped>
    @import '../assets/style/vars.scss';

    .wrapper{
        display: flex;
        flex-wrap: wrap;
        padding: 50px;
        justify-content: space-evenly;
        row-gap: 50px;
    }
</style>