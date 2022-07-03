<template>
  <div>
    <div>
      <input
        type="text"
        placeholder="Search movies"
        v-model="query"
        v-on:change="searchMovies"
      />
      <span href="#!">&#128269;</span>
    </div>
    <div class="d-flex flex-wrap" id="movieContainer">
      <!-- <div class="flex-fill"> -->
      <b-card
        v-for="(movie, index) in movies"
        :key="index"
        v-bind:title="movie.title"
        v-bind:img-src="'https://image.tmdb.org/t/p/w200/' + movie.poster_path"
        img-alt="Image"
        img-top
        tag="article"
        style="max-width: 20rem"
        class="mb-2"
      >
        <!-- {{movie}} -->
        <MovieCard :movie-prop="movie"></MovieCard>
      </b-card>
    </div>
    <!-- </div> -->
    <nav v-if="resultType == 'popular'" style="margin-bottom:2em">
      <ul class="pagination">
        <li class="page-item">
          <button
            type="button"
            class="page-link"
            v-if="currentPage != 1"
            @click="currentPage--"
          >
            Previous
          </button>
        </li>
        <li class="page-item">
          <button
            type="button"
            class="page-link"
            v-for="pageNumber in pageRange.slice(
              currentPage - 1,
              currentPage + 5
            )"
            :key="pageNumber"
            @click="currentPage = pageNumber"
          >
            {{ pageNumber }}
          </button>
        </li>
        <li class="page-item">
          <button
            type="button"
            @click="currentPage++"
            v-if="currentPage < totalPages"
            class="page-link"
          >
            Next
          </button>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
import MovieCard from "./MovieCard.vue";
export default {
  components: { MovieCard },
  name: "ContentPage",
  data() {
    return {
      name: "Martin's Movies",
      query: null,
      movies: [],

      currentPage: 1,
      totalPages: 1,

      resultType: "popular",
      // pageRange: _.range(this.currentPage, this.totalPages),
    };
  },
  computed: {
    pageRange() {
      var pageRange = [];
      for (var i = this.currentPage; i <= this.totalPages; i++) {
        pageRange.push(i);
      }

      return pageRange;
    },
  },
  watch: {
    // whenever question changes, this function will run
    currentPage(newPage, oldPage) {
      if (this.resultType === "popular") this.fetchMovies();
    },
  },
  methods: {
    fetchMovies() {
      this.resultType = "popular";
      const API_KEY = "1e448e0dfcdbb565f5d329820065b4d2";

      const pageNumber = this.currentPage;
      let promise = fetch(
        "https://api.themoviedb.org/3/movie/popular?api_key=" +
          API_KEY +
          "&language=en-US&page=" +
          pageNumber
      );
      console.log(
        "https://api.themoviedb.org/3/movie/popular?api_key=" +
          API_KEY +
          "&language=en-US&page=" +
          pageNumber
      );
      let jsonPromise = promise.then(function (response) {
        return response.json();
      });
      jsonPromise.then((jsonData) => {
        console.log(jsonData);
        this.movies = jsonData.results;
        this.currentPage = jsonData.page;
        this.totalPages = jsonData.total_pages;
      });
    },

    searchMovies() {
      const searchQuery = this.query;
      if (searchQuery) {
        this.resultType = "search";
        const API_KEY = "1e448e0dfcdbb565f5d329820065b4d2";

        let promise = fetch(
          "https://api.themoviedb.org/3/search/movie?api_key=" +
            API_KEY +
            "&query=" +
            searchQuery
        );

        let jsonPromise = promise.then(function (response) {
          return response.json();
        });
        jsonPromise.then((jsonData) => {
          console.log(jsonData);
          this.movies = jsonData.results;
          // this.currentPage = jsonData.page;
          // this.totalPages = jsonData.total_pages;
        });
      } else {
        this.currentPage = 1;
        this.fetchMovies();
      }
    },
  },
  mounted() {
    this.fetchMovies();
    // this.searchMovies();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style scoped>
#movieContainer {
  margin: 3em 3em 3em 6em;
}

h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

button.page-link {
  display: inline-block;
}
button.page-link {
  font-size: 17px;
  color: black;
  font-weight: 600;
}
.offset {
  width: 500px !important;
  margin: 20px auto;
}
input{
  margin-top: 1.2em;
  border-radius: 5px;
  border: 1px solid #e3e3e3;
  width: 30em;
  height:3em;
  background-color:  #e3e3e3;
  padding-left: 20px;
}
</style>
