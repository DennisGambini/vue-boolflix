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
        }
    },
    computed:{
        movieFounded(){
            let checker = this.movieCards.length === 0 ? false : true
            return checker
        },
        seriesFounded(){
            let checker = this.seriesCards.length === 0 ? false : true
            return checker
        }
    },
    methods:{
        callBothApi(){
            this.callApi('movie')
            this.callApi('tv')
        },
        callApi(type){
            this.myQuery = this.writtenText;
            axios.get(`${this.apiUrl}/search/${type}/?api_key=${this.myApiKey}&query=${this.myQuery}&language=it-IT`)
            .then((res) => {
            console.log(res.data.results)
            // controllo lunghezza
            if(res.data.results.length > this.previewNumber){
                res.data.results.splice(this.previewNumber)
            }
            // divido per tipo
            switch (type){
                case 'movie':
                    this.movieCards = [...res.data.results];
                    break;
                default:
                    this.seriesCards = [...res.data.results];
                    break;
            }
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