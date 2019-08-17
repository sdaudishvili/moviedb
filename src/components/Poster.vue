<template>
    <div id="poster" v-if="movieObj!=''">
        <div id="imgCont">
            <img id="posterImg" v-bind:src="'https://image.tmdb.org/t/p/w500' + movieObj.poster_path">
        </div>
        <div id="details">
            <h1>{{movieObj.title}}</h1>
            <p id="tagline" v-if="movieObj.tagline !=''">{{movieObj.tagline}}</p>
            <div id="overview">
            <p id="overview">{{movieObj.overview}}</p>
            </div>
            <table>
                <tbody>
                    <tr>
                        <td id="metascore">
                            <img src="../assets/imgsrc/imdb.svg"><img>
                            <div class="topLabel">METASCORE</div>
                            <div class="botLabel">metascore</div>
                        <td id="popularity">
                            <img src="../assets/imgsrc/popularity.svg"><img>
                            <div class="topLabel">POPULARITY</div>
                            <div class="botLabel">{{movieObj.popularity}}</div>
                        </td>
                    </tr>
                    <tr>
                        <td id="genres">
                            <div class="topLabel">GENRE</div>
                            <div v-if="movieObj.genres.length != 0" class="botLabel">{{movieObj.genres[0].name}}</div>
                        </td>
                        <td id="runtime">
                            <div class="topLabel">RUNTIME</div>
                            <div class="botLabel">{{movieObj.runtime}} minutes</div>
                        </td>
                    </tr>
                    <tr>
                        <td id="revenue">
                            <div class="topLabel">REVENUE</div>
                            <div class="botLabel">${{formatRevenue(movieObj.revenue)}}</div>
                        </td>
                        <td id="vote">
                            <div class="topLabel">VOTE AVERAGE</div>
                            <!-- <div class="botLabel">{{movieObj.vote_average}}</div> -->
                            <div class="star-ratings-sprite">
                                <span :style="{width: getRating(movieObj.vote_average)}" class="star-ratings-sprite-rating">
                            </span></div>
                        </td>
                    </tr>
                </tbody>
            </table>
            
            
        </div>
        <div style="clear:both height: 0px overflow: hidden"></div>
        <div id="backgroundImgCont">
            <img id="backgroundImg" v-bind:src="'https://image.tmdb.org/t/p/original' + movieObj.backdrop_path">
        </div>

    </div>
</template>

<script>
export default {
    name: 'Poster',
    props: [
        'movieObj'
    ],
    data() {
        return {
            imgBaseUrl: 'https://image.tmdb.org/t/p/w500',
            revenue: ''
        }
    },

    computed: {
        imgUrl() {
            return this.imgBaseUrl + this.movieObj.poster_path
        },
    },
    methods: {
        formatRevenue(value) {
            let val = (value/1)
            return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".")
        },
        getRating(value){
            var x = value * 10;
            x += '%';
            return x;
        }
    }
}
</script>

<style>

@import '../assets/style/style.css';
</style>