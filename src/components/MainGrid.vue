<template>
    <section>
        <h2 v-if="writtenText">Film</h2>
        <div v-if="writtenText" class="wrapper">
            <app-card class="card" v-for="(card, index) in movieCards" 
            :key="index" 
            :card="card" 
            :imgUrl="imgUrl" 
            :titleProp="card.title" 
            :originalTitleProp="card.original_title"
            :necessary="checkTitles(card.title, card.original_title)"/>
        </div>

        <h2 v-if="writtenText">Serie TV</h2>
        <div v-if="writtenText" class="wrapper">
            <app-card class="card" v-for="(card, index) in seriesCards" 
            :key="index" 
            :card="card" 
            :imgUrl="imgUrl" 
            :titleProp="card.name" 
            :originalTitleProp="card.original_name"
            :necessary="checkTitles(card.name, card.original_name)"/>
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
            apiUrl: 'https://api.themoviedb.org/3',
            imgUrl:'https://image.tmdb.org/t/p',
            myApiKey: '2ef36b734d4be91dd7af56b7d0142468',
            myQuery: '',
            movieCards:[],
            seriesCards:[]
        }
    },
    methods:{
        callBothApi(){
            this.callApiMovie();
            this.callApiSeries();
        },
        callApiMovie(){
            this.myQuery = this.writtenText;
            axios.get(`${this.apiUrl}/search/movie/?api_key=${this.myApiKey}&query=${this.myQuery}&language=it-IT`)
            .then((res) => {
            console.log(res.data.results)
            this.movieCards = [...res.data.results]
            })
            .catch((err) => {
            console.log(err);
            })         
        },
        callApiSeries(){
            this.myQuery = this.writtenText;
            axios.get(`${this.apiUrl}/search/tv/?api_key=${this.myApiKey}&query=${this.myQuery}`)
            .then((res) => {
            console.log(res.data.results)
            this.seriesCards = [...res.data.results]
            })
            .catch((err) => {
            console.log(err);
            })
        },
        checkTitles(a, b){
            return a === b ? false : true;
        }
        
    },
    updated(){
        if(this.myQuery !== this.writtenText){
            this.callBothApi()
        }
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
    h2{
        text-align: center;
        color: white;
        text-transform: uppercase;
    }
</style>