<template>
  <div>
    <h4 class="has-text-success has-text-centered" v-if="loading">
      <span class="icon">
        <i class="fas fa-spin fa-spinner"></i>
      </span>
      Loading Movies...
    </h4>
    <div class="columns is-multiline" v-if="movies && movies.length">
      <div class="column is-one-third" v-for="(movie, index) in movies" :key="index">
        <div class="card">
          <div class="card-image">
            <figure class="image is-4by3">
              <img
                :src="movie.image === null ? 'https://cdn1.thr.com/sites/default/files/imagecache/landscape_928x523/2012/11/movie_theater_interior_a_l.jpg' : movie.image"
                :alt="movie.title"
              >
            </figure>
          </div>
          <div class="card-content">
            <div class="media">
              <div class="media-left">
                <figure class="image is-48x48">
                  <img
                    :src="movie.image === null ? 'https://cdn1.thr.com/sites/default/files/imagecache/landscape_928x523/2012/11/movie_theater_interior_a_l.jpg' : movie.image"
                    :alt="movie.title"
                  >
                </figure>
              </div>
              <div class="media-content">
                <p class="title is-4">{{ movie.title }}</p>
                <p class="subtitle is-6">{{ movie.genre }}</p>
              </div>
            </div>

            <div class="content">
              {{ movie.synopsis }}
              <br>
              <time :datetime="movie.created_at" v-text="movie.created_at"></time>
            </div>
          </div>
          <footer class="card-footer">
            <a href="#" class="card-footer-item">Edit</a>
            <a href="#" class="card-footer-item is-danger">Delete</a>
          </footer>
        </div>
      </div>
    </div>
    <div v-else class="has-text-centered">No movies yet.</div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        loading: true,
        movies: []
      };
    },
    created() {
      setTimeout(() => {
        this.fetchMovies();
      }, 1000);
    },
    methods: {
      fetchMovies() {
        fetch("https://simplecrudapi.herokuapp.com/api/movies")
          .then(res =>
            res.json().then(movies => {
              this.movies = movies;
              this.loading = !this.loading;
            })
          )
          .catch(err => console.log(err));
      }
    }
  };
</script>
