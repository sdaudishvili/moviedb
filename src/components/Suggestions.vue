<template>
    
    <div class="a">
        <input autocomplete="off" v-model="movieName" v-on:keyup="getInput()"
                    type="text" id="search-field" placeholder="Enter the movie name...">
        <table v-if="movieName != ''">
            <tbody v-bind:key="movie" v-for="movie in info.results">
                <tr class="autocomplete-result" v-if="checkTitle(movie.title)" v-on:click="getMovie(movie)">
                    <td>{{movie.title}}</td>
                </tr>
            </tbody>
        </table>
    </div>

</template>

<script>


export default {
    name: 'Suggestions',
    props: [

    ],
    data(){
        return {
            movieName: '',
            baseUrl: "https://api.themoviedb.org/3/search/movie?api_key=9e2168f32202773e09b57af0e9187563&query=",
            info: '',
            selected: false,
            movieDetails: ''
        }
    },
    computed: {
        apiUrl() {
            return this.baseUrl + this.movieName
        }
    },
    methods: {
        getInput: function(){
            this.selected = false;
            if(this.movieName != ''){
                if(!this.selected){
                    this.axios.get(this.apiUrl)
                    .then((response) => {
                        this.info = response.data;
                    })
                }
            }
        },

        checkTitle: function(title){
            if(this.movieName.toLowerCase() == title.substr(0,this.movieName.length).toLowerCase()){
                return true;
            }
            return false;
        },
        getMovie: function(movie){
            this.movieName = movie.title
            var url = 'https://api.themoviedb.org/3/movie/' + movie.id + '?api_key=9e2168f32202773e09b57af0e9187563';
            this.info = '';
            this.selected = true;

            this.axios.get(url)
            .then((response) => {
                this.movieDetails = response.data;
                this.$emit('movie', this.movieDetails);
            })
            
        }
    }

}
</script>


<style>


@import '../assets/style/style.css';
</style>