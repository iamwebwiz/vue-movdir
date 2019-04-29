<template>
  <div>
    <div class="modal" id="editMovieModal">
      <div class="modal-background"></div>
      <div class="modal-card">
        <header class="modal-card-head">
          <p class="modal-card-title">Edit Movie Info</p>
          <button class="delete" aria-label="close" @click="closeModal"></button>
        </header>
        <section class="modal-card-body">
          <div class="field">
            <label class="label" for="title">Title</label>
            <div class="control">
              <input
                type="text"
                id="title"
                class="input"
                placeholder="Movie Title"
                v-model="movie.title"
              >
            </div>
          </div>

          <div class="field">
            <label class="label" for="genre">Genre</label>
            <div class="control">
              <input type="text" id="genre" placeholder="Genre" v-model="movie.genre" class="input">
            </div>
          </div>

          <div class="field">
            <label class="label" for="synopsis">Synopsis</label>
            <div class="control">
              <textarea
                placeholder="Synopsis"
                id="synopsis"
                v-model="movie.synopsis"
                class="textarea"
              ></textarea>
            </div>
          </div>
        </section>
        <footer class="modal-card-foot">
          <button class="button is-success" @click="onMovieUpdate" :disabled="updating">
            <span class="icon" v-show="updating">
              <i class="fas fa-spin fa-spinner"></i>
              &nbsp;
            </span>
            Save changes
          </button>
          <button class="button" @click="closeModal">Cancel</button>
        </footer>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: ["movie", "updating", "onMovieUpdate"],
    methods: {
      closeModal() {
        document.querySelector("#editMovieModal").classList.remove("is-active");
        document.querySelector("html").classList.remove("is-clipped");
      }
    }
  };
</script>
