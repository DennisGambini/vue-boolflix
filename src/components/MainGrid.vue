<template>
    <section>
        <app-loader class="loader" v-if="loading" />

        <div role="checker" v-if="writtenText && !loading && movieFounded">
            <h2>{{movies}}</h2>
            <div class="wrapper">
                <app-card class="card" v-for="(card, index) in movieCards" 
                :key="index" 
                :card="card" 
                :imgUrl="imgUrl" 
                :titleProp="card.title" 
                :originalTitleProp="card.original_title"
                :necessary="checkTitles(card.title, card.original_title)"/>
            </div>
        </div>
        <div v-else-if="!loading" class="warning">
            <div>    
                <h2>nessuna film trovato!</h2>
                <p>riprova con un altra ricerca</p>
            </div>
        </div>

        <div role="checker" v-if="writtenText && !loading && seriesFounded">
            <h2>{{series}}</h2>
            <div class="wrapper">
                <app-card class="card" v-for="(card, index) in seriesCards" 
                :key="index" 
                :card="card" 
                :imgUrl="imgUrl" 
                :titleProp="card.name" 
                :originalTitleProp="card.original_name"
                :necessary="checkTitles(card.name, card.original_name)"/>
            </div>
        </div>
        <div v-else-if="!loading" class="warning">
            <div>
                <h2>nessuna serie trovata!</h2>
                <p>riprova con un altra ricerca</p>
            </div>
        </div>

    </section>
</template>

<script>
import axios from 'axios'
import AppCard from './AppCard.vue';
import AppLoader from './AppLoader.vue';

export default {
  components: { AppCard, AppLoader },

    name: 'MainGrid',
    props:{
        writtenText: String,
        myDefault: String,
        movies: String,
        series: String,
        previewNumber: Number
    },
    data(){
        return{
            apiUrl: 'https://api.themoviedb.org/3',
            imgUrl:'https://image.tmdb.org/t/p',
            myApiKey: '2ef36b734d4be91dd7af56b7d0142468',
            myQuery: '',
            movieCards:[],
            seriesCards:[],
            loading: false,
            movieFounded: true,
            seriesFounded: true
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
            if(this.movieCards.length > this.previewNumber){
                this.movieCards.splice(this.previewNumber)
            }
            this.movieCards.length === 0 ? this.movieFounded = false : this.movieFounded = true;
            setTimeout(()=>{
                this.loading = false;
            }, 500)
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
            if(this.seriesCards.length > this.previewNumber){
                this.seriesCards.splice(this.previewNumber)
            }
            this.seriesCards.length === 0 ? this.seriesFounded = false : this.seriesFounded = true;
            setTimeout(()=>{
                this.loading = false;
            }, 500)
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
            this.loading = true;
            setTimeout(this.callBothApi, 500)
        }
    },
    mounted(){
        if(this.myDefault){
            this.loading = true;
            setTimeout(this.callBothApi, 500)
        }
    }
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
        color: $text-color;
        text-transform: uppercase;
    }
    .warning{
        height: calc(100vh / 2.5);
        width: calc(100vh / 2.5);
        background: radial-gradient(circle, $bg-header 0%, $bg-body 60%);
        margin: 0 auto;
        @include flex-row-center-center;
        div{
            h2{
                color: $text-warn;
            }
            p{
                color: $text-color;
                text-align: center;
            }
        }
    }
    
</style>