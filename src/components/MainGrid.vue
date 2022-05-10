<template>
  <section>
      <!-- <div v-if="writtenText" class="card">
          <div class="title">{{movie.original_title}}</div>
          <img :src="imgUrl + '/original' + movie.poster_path" 
            :alt="movie.original_title + ' poster'">
      </div> -->

        <div v-if="writtenText" class="wrapper">
            <div v-for="(card, index) in cards" :key="index" class="card">
          <div class="title">{{card.original_title}}</div>
          <img :src="imgUrl + '/original' + card.poster_path" 
            :alt="card.original_title + ' poster'">
      </div>
        </div>
      

  </section>
</template>

<script>
import axios from 'axios'

export default {

    name: 'MainGrid',
    props:{
        writtenText: String,
        textEvent: Event
    },
    data(){
        return{
            movie: {},
            apiUrl: 'https://api.themoviedb.org/3',
            imgUrl:'https://image.tmdb.org/t/p',
            myApiKey: '2ef36b734d4be91dd7af56b7d0142468',
            myQuery: '',
            cards:[]
        }
    },
    methods:{
        // setQuery(text){
        //     this.myQuery = text;
        //     this.callApi()
        // },
        callApi(){
            if(this.myQuery !== this.writtenText){
                this.myQuery = this.writtenText;
                axios.get(`${this.apiUrl}/search/movie/?api_key=${this.myApiKey}&query=${this.myQuery}&lang=it-IT`)
                .then((res) => {
                //console.log(res.data.results[0]);
                //this.movie = {...res.data.results[0]};
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
        flex-wrap: wrap
    }
    .card{
        @include flex-column-between;
        gap: 20px;
        width: 220px;
        color: white;
        background-color: $bg-card;
        img{
            width: 100%;
        }
    }
</style>