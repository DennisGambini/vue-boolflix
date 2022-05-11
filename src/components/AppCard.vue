<template>
    <div class="card">

        <img :src="imgUrl + '/original' + card.poster_path" 
            :alt="card.original_title + ' poster'">

        <div class="description">
            <div class="title">
                <span>Titolo: </span>
                {{titleProp}}
            </div>
            <div>
                <div class="overview" :title="card.overview">
                    <span>Overview: </span>
                    {{card.overview === "" ? 'Sorry! Not available' : breakOverview(card.overview) + '...'}}
                    <i v-if="card.overview === '' " class="fa-solid fa-face-sad-cry"></i>
                </div>
                <div class="original_title" v-if="necessary">
                    <span>Titolo originale: </span>
                    {{originalTitleProp}}
                </div>
                <div class="language">
                    <span>Lingua originale: </span>    
                    {{card.original_language}}
                    <img :src="'https://countryflagsapi.com/png/' + `${card.original_language === 'en' ? 'gb' : card.original_language}`" :alt="card.original_language + ' flag'"/>
                    </div>
            </div>
            <div class="vote">
                <span>Voto: </span>
                {{card.vote_average}}
                <i v-if="manipulateVote(card.vote_average) >= 1" class="fa-solid fa-star-of-david"></i>
                <i v-if="manipulateVote(card.vote_average) >= 2" class="fa-solid fa-star-of-david"></i>
                <i v-if="manipulateVote(card.vote_average) >= 3" class="fa-solid fa-star-of-david"></i>
                <i v-if="manipulateVote(card.vote_average) >= 4" class="fa-solid fa-star-of-david"></i>
                <i v-if="manipulateVote(card.vote_average) >= 5" class="fa-solid fa-star-of-david"></i>
            </div>
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
        originalTitleProp: String,
        necessary: Boolean
    },
    methods:{
        breakOverview(text){
            const array = text.split("", 200);
            const newWord = array.join('');
            return newWord;
        },
        manipulateVote(vote){
            let splitNumber;
            if(vote % 2 === 0){
                splitNumber = (vote / 2) + 1;
                return splitNumber;
            } else {
                vote = vote / 2;
                let newVote = vote.toString()
                if(newVote.length !== 1){
                    splitNumber = parseInt(newVote.split('', 1)) + 1
                }
                return splitNumber;
            }
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
        border-radius: $card-radius;
        overflow: hidden;
        position: relative;
        box-shadow: 2px 2px 4px $bg-header;
        font-size: $card-font-size;
        > img{
            // height: 290px;
            height: 100%;
            width: 100%;
            object-fit: cover;
            object-position: center;
            border-radius: $card-radius;
        }
        .description{
            display: none;
            gap: 20px;
            position: absolute;
            top: 0;
            left: 0;
            bottom: 0;
            right: 0;
            background: rgba($color: $bg-header, $alpha: 0.95);
            padding: 20px;
            span{
                color: red;
                text-transform: uppercase;
            }
            .overview{
                i{
                    color: $star-color;
                }
            }
            .language{
                img{
                    vertical-align: middle;
                    @include flag-size
                }
            }
            .vote{
                i{
                    color: $star-color;
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