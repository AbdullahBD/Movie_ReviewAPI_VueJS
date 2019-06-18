<template>
    <div class="card">
        <img v-if="movie.multimedia"
            :src="movie.multimedia.src"
            class="card-img-top"
            :alt="movie.headline">
        <img v-else src="https://via.placeholder.com/400x270"
            class="card-img-top" 
            :alt="movie.display_title">

        <div class="card-body">
            <h5 class="card-title"><b>{{movie.display_title}}</b></h5>
            <p>
                <span class="badge badge-primary">Published: {{ movie.publication_date}}</span>
                <span class="badge badge-info">Opening: {{ movie.opening_date}}</span>
                <span class="badge badge-default">Reviews: {{ movie.critics_pick}}</span>
                <span class="badge badge-default">Rating: {{ movie.mpaa_rating}}</span>
            </p>
            <p class="card-text">{{movie.summary_short}}</p>
            <a :href="movie.link.url" target="_blank" class="btn btn-primary">Detail</a>
        </div>
    </div>
</template>

<script>
export default {
    name: 'movie',
    props: {
        movie: {
            type: Object,
            required: true,
            default: () => {}
        }
    }
}
</script>

