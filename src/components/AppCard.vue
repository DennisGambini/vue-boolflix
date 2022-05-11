<template>
    <div class="card">

        <img :src="imgUrl + '/original' + card.poster_path" 
            :alt="card.original_title + ' poster'">

        <div class="description">
            <div class="title"><span>Titolo: </span>{{titleProp}}</div>
            <div>
                <div class="overview"><span>Overview: </span>{{breakOverview(card.overview) + '...'}}</div>
                <div class="original_title"><span>Titolo originale: </span>{{originalTitleProp}}</div>
                <div class="language">
                    <span>Lingua originale: </span>
                    {{card.original_language}}
                    <img :src="'https://countryflagsapi.com/png/' + `${card.original_language === 'en' ? 'gb' : card.original_language}`" :alt="card.original_language + ' flag'"/>
                    </div>
            </div>
            <div class="vote"><span>Voto: </span>{{card.vote_average}}</div>
        </div>


    </div>
</template>

<script>
export default {
    name: 'AppCard',
    props:{
        card: Object,
        imgUrl: String,
        titleProp: String,
        originalTitleProp: String
    },
    methods:{
        breakOverview(text){
            const array = text.split("", 200);
            const newWord = array.join('')
            return newWord
        }
    }
}
</script>

<style lang="scss" scoped>
@import '../assets/style/vars.scss';

.card{
        @include flex-column-between;
        gap: 20px;
        height: 350px;
        width: 250px;
        padding: 10px;
        color: white;
        background-color: $bg-card;
        border-radius: 10px;
        overflow: hidden;
        overflow-y: auto;
        position: relative;
        box-shadow: 2px 2px 4px $bg-header;
        img{
            height: 290px;
        }
        .description{
            display: none;
            gap: 20px;
            position: absolute;
            top: 0;
            left: 0;
            bottom: 0;
            right: 0;
            background: rgba($color: $bg-header, $alpha: 0.8);
            padding: 20px;
            span{
                color: red;
            }
            .language{
                img{
                    @include flag-size
                }
            }
        }
        &:hover{
            .description{
                @include flex-column-center;
            }
        }
    }


</style>