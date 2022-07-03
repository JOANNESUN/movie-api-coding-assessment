<template>
  <div>
    <b-card-text>
      {{ movieProp.overview }}
    </b-card-text>

    <b-button :href="'https://www.imdb.com/title/'+imdbId" variant="primary"
      >Read More</b-button
    >
  </div>
</template>

<script>
export default {
  data() {
    return {
      query: null,
      imdbId: null
    };
  },
  props: ["movie-prop"],
  methods: {
    //get API
    fetchMovieDetail(movieId) {
      const API_KEY = "1e448e0dfcdbb565f5d329820065b4d2";

      let promise = fetch(
        "https://api.themoviedb.org/3/movie/" +
          movieId +
          "?api_key=" +
          API_KEY +
          "&language=en-US&page=1"
      );

      let jsonPromise = promise.then(function(response) {
        return response.json();
      });

      jsonPromise.then(jsonData => {
        this.imdbId = jsonData.imdb_id;
      });
    }
  },
  updated() {
    var movieId = this.$props.movieProp.id;
    this.fetchMovieDetail(movieId)
  }
};
</script>

<style>

.btn{
position: absolute;
right:    0;
bottom:   10px;
right: 6px;

}

.btn-primary{
    background-color: rgb(163, 115, 211);
    border-color:rgb(163, 115, 211);
}
</style>
