<template>
  <div class="movie-wrapper" :style="styles">
    <div class="movie-info">
      <h1>{{movie.title}}</h1>
      <h3>Release Date: {{flipDate}}</h3>
      <p>{{movie.overview}}</p>
    </div>
  </div>
</template>

<script>
const BACKDROP_PATH = "https://image.tmdb.org/t/p/w1280";

export default {
  data() {
    return {
      movie: {}
    };
  },
  created: function() {
    this.fetchData();
  },
  computed: {
    styles() {
      return {
        background: `url(${BACKDROP_PATH}${this.movie.backdrop_path}) no-repeat center`
      };
    },
    flipDate: function() {
      let date = this.movie.release_date;
      return (date = date
        .split("-")
        .reverse()
        .join("-"));
    }
  },
  methods: {
    fetchData: async function() {
      try {
        const res = await fetch(
          `https://api.themoviedb.org/3/movie/${this.$route.params.id}?api_key=a7682595368d262d972b855b56eab5c5`
        );
        const movie = await res.json();
        this.movie = movie;
      } catch (e) {
        console.log(e);
      }
    }
  }
};
</script>

<style scoped>
.movie-wrapper {
  position: relative;
  padding-top: 60vh;
}

.movie-info {
  background: #fff;
  color: #222;
  padding: 2rem 10%;
}
</style>