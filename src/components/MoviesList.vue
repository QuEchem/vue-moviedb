<template>
  <ul>
    <li v-for="movie in movies" :key="movie.id">
      <Movie :movie="movie" />
    </li>
  </ul>
</template>

<script>
import Movie from "./Movie.vue";

export default {
  name: "MoviesList",
  data() {
    return {
      movies: [],
      API: process.env.VUE_APP_API_KEY
    };
  },
  created: function() {
    this.fetchData();
  },
  methods: {
    fetchData: async function() {
      try {
        const res = await fetch(
          `https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=${this.API}`
        );
        const movies = await res.json();
        this.movies = movies.results;
      } catch (e) {
        console.log(e);
      }
    }
  },
  components: {
    Movie
  }
};
</script>

<style scoped>
ul {
  display: grid;
  list-style: none;
  padding: 1 rem;
  margin: 0;
  grid-row-gap: 1rem;
  grid-template-columns: repeat(6, 1fr);
}
</style>