<template>
  <div>
    <div class="modal" id="newMovieModal">
      <div class="modal-background"></div>
      <div class="modal-card">
        <header class="modal-card-head">
          <p class="modal-card-title">Add New Movie</p>
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
                v-model="newMovie.title"
              >
            </div>
          </div>

          <div class="field">
            <label class="label" for="genre">Genre</label>
            <div class="control">
              <input type="text" id="genre" placeholder="Genre" v-model="newMovie.genre" class="input">
            </div>
          </div>

          <div class="field">
            <label for="image" class="label">Image</label>
            <div class="file is-info">
              <label class="file-label">
                <input
                  class="file-input"
                  type="file"
                  ref="image"
                  accept="image/*"
                  @change="handleImageChange"
                >
                <span class="file-cta">
                  <span class="file-icon">
                    <i class="fas fa-upload"></i>
                  </span>
                  <span class="file-label">Choose a file…</span>
                </span>
              </label>
            </div>
          </div>

          <div class="field">
            <label class="label" for="synopsis">Synopsis</label>
            <div class="control">
              <textarea
                placeholder="Synopsis"
                id="synopsis"
                v-model="newMovie.synopsis"
                class="textarea"
              ></textarea>
            </div>
          </div>
        </section>
        <footer class="modal-card-foot">
          <button class="button is-info" @click="addMovie" :disabled="adding">
            <span class="icon" v-show="adding">
              <i class="fas fa-spin fa-spinner"></i>
              &nbsp;&nbsp;
            </span>
            Save
          </button>
          <button class="button" @click="closeModal">Cancel</button>
        </footer>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: ["newMovie", "adding", "closeModal", "addMovie"],
    methods: {
      handleImageChange() {
        this.newMovie.image = this.$refs.image.files[0];
      }
    }
  };
</script>
