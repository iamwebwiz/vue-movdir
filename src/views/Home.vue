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
              <br>Added on:
              <time :datetime="movie.created_at" v-text="creationDate(movie.created_at)"></time>
            </div>
          </div>
          <footer class="card-footer">
            <a
              href="javascript:;"
              class="card-footer-item has-text-primary"
              @click="editMovie(index)"
            >Edit</a>
            <a
              href="javascript:;"
              class="card-footer-item has-text-danger"
              @click="deleteMovie(index)"
            >Delete</a>
          </footer>
        </div>
      </div>
    </div>
    <div v-else class="has-text-centered">No movies yet.</div>

    <EditMovie :movie="movie" :updating="updating" :onMovieUpdate="updateMovie"></EditMovie>
  </div>
</template>

<script>
  import moment from "moment";
  import axios from "axios";
  import swal from "sweetalert";

  import EditMovie from "./EditMovie";

  export default {
    components: {
      EditMovie
    },
    data() {
      return {
        loading: true,
        movies: [],
        moment: moment,
        updating: false,
        movie: {}
      };
    },
    created() {
      setTimeout(() => {
        this.fetchMovies();
      }, 1000);
    },
    methods: {
      fetchMovies() {
        axios
          .get("https://simplecrudapi.herokuapp.com/api/movies")
          .then(res => {
            this.movies = res.data;
            this.loading = !this.loading;
          })
          .catch(err => console.log(err.response));
      },
      deleteMovie(index) {
        swal({
          title: "Are you sure?",
          text: "This action cannot be reversed. Proceed?",
          icon: "warning",
          buttons: true,
          dangerMode: true
        }).then(willDelete => {
          if (willDelete) {
            let movie = this.movies[index];
            axios
              .delete(
                `https://simplecrudapi.herokuapp.com/api/movies/${movie.id}`
              )
              .then(res => {
                this.movies.splice(index, 1);
                swal(res.data, {
                  icon: "success"
                });
              })
              .catch(err => console.log(err.response));
          } else {
            //
          }
        });
      },
      creationDate(date) {
        return moment(date).format("DD/MM/YYYY");
      },
      editMovie(index) {
        let movie = this.movies[index];
        this.movie = movie;
        let html = document.querySelector("html");
        let modal = document.querySelector("#editMovieModal");
        modal.classList.add("is-active");
        html.classList.add("is-clipped");

        modal.querySelector(".modal-background").addEventListener("click", e => {
          modal.classList.remove("is-active");
          html.classList.remove("is-clipped");
        });
      },
      updateMovie() {
        let movie = this.movie;
        this.updating = !this.updating;
        axios
          .put(`https://simplecrudapi.herokuapp.com/api/movies/${movie.id}`, {
            title: movie.title,
            genre: movie.genre,
            synopsis: movie.synopsis
          })
          .then(res => {
            swal("Success!", res.data, "success");
            this.updating = !this.updating;
            document
              .querySelector("#editMovieModal")
              .classList.remove("is-active");
            document.querySelector("html").classList.remove("is-clipped");
          })
          .catch(err => console.log(err.response));
      }
    }
  };
</script>
