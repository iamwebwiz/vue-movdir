<template>
  <div id="app">
    <section class="hero">
      <div class="hero-body">
        <div class="container">
          <div class="level">
            <div class="level-left">
              <div class="level-item">
                <h1 class="title has-text-success">
                  <span class="icon">
                    <i class="fas fa-video"></i>
                  </span>
                  &nbsp;
                  Vue Movies CRUD
                </h1>
              </div>
              <div class="level-item">
                <h2 class="subtitle">Manage Movies in one place</h2>
              </div>
            </div>
            <div class="level-right">
              <div class="level-item">
                <button class="button is-info" @click="addNewMovie">Add Movie</button>
              </div>
            </div>
          </div>
          <hr>
          <Home/>
        </div>
      </div>
    </section>

    <NewMovie :movie="movie" :addMovie="addMovie" :adding="adding" :closeModal="closeModal"></NewMovie>
  </div>
</template>

<script>
  import axios from "axios";
  import swal from "sweetalert";

  import Home from "./views/Home";
  import NewMovie from "./views/NewMovie";

  export default {
    components: {
      Home,
      NewMovie
    },
    data() {
      return {
        adding: false,
        movie: {
          title: "",
          genre: "",
          synopsis: "",
          image: ""
        }
      };
    },
    methods: {
      addNewMovie() {
        document.querySelector("#newMovieModal").classList.add("is-active");
        document.querySelector("html").classList.add("is-clipped");

        document
          .querySelector("#newMovieModal")
          .querySelector(".modal-background")
          .addEventListener("click", e => {
            document
              .querySelector("#newMovieModal")
              .classList.remove("is-active");
            document.querySelector("html").classList.remove("is-clipped");
          });
      },
      closeModal() {
        document.querySelector("#newMovieModal").classList.remove("is-active");
        document.querySelector("html").classList.remove("is-clipped");
      },
      resetForm() {
        this.movie = { title: "", genre: "", synopsis: "", image: "" };
      },
      addMovie() {
        this.adding = !this.adding;
        const CORS = "https://cors-anywhere.herokuapp.com/";

        axios
          .post(CORS + "https://simplecrudapi.herokuapp.com/api/movies/new", {
            title: this.movie.title,
            genre: this.movie.genre,
            synopsis: this.movie.synopsis,
            image: this.movie.image
          })
          .then(res => {
            swal("Success!", res.data, "success");
            this.resetForm();
            this.adding = !this.adding;
            this.closeModal();
          })
          .catch(err => {
            console.log(err.response);
            this.resetForm();
            this.adding = !this.adding;
          });
      }
    }
  };
</script>
