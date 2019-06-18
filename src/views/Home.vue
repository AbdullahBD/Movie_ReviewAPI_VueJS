<template>
    <div>
        <div class="row">
            <div class="col-sm-6">
                <h3 class="text-left"><b>Movie List from NYTimes</b></h3>
            </div>
            <div class="col-sm-6">
                <form class="form-inline" @submit.prevent="submitMovieSearch">
                    <div class="form-group">
                        <input type="text" v-model="searchMovie" class="form-control" placeholder="Input movie name">
                    </div>
                    <button type="submit" class="btn btn-primary">Search Movie</button>
                </form>
            </div>
        </div>
        <hr>
        <div class="row">
            <template v-if="movies">
                <div v-for="(movie, index) in movies" :key="index" class="col-sm-4">
                    <movie :movie="movie"></movie>
                </div>
            </template>
            <div v-else class="spinner-border" role="status">
                <span class="sr-only">Loading...</span>
            </div>
        </div>
    </div>
</template>

<script>
// @ is an alias to /src
import Movie from '@/components/Movie.vue'
import axios from "axios";

export default {
    name: 'home',
    components: {
        Movie
    },
    data() {
        return {
            movies: [],
            searchMovie: ''
        }
    },
    mounted() {
        this.fetchMovie();
    },
    methods: {
        fetchMovie() {
            axios.get('https://api.nytimes.com/svc/movies/v2/reviews/search.json?&api-key=l6STMygHQLofbYJKoGCNCXQjuHGUY5os')
            .then(response => {
                this.movies = response.data.results
                console.log(response)
            });
        },
        submitMovieSearch() {
            axios.get('https://api.nytimes.com/svc/movies/v2/reviews/search.json?query=' + this.searchMovie + '&api-key=l6STMygHQLofbYJKoGCNCXQjuHGUY5os')
            .then(response => {
                this.movies = response.data.results
                console.log(response)
            });
        }
    }
}
</script>
