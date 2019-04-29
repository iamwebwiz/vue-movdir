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
          <!-- Content ... -->
        </section>
        <footer class="modal-card-foot">
          <button class="button is-success">Save changes</button>
          <button class="button" @click="closeModal">Cancel</button>
        </footer>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "EditMovie",
    props: ["movie"],
    methods: {
      closeModal() {
        document.querySelector("#editMovieModal").classList.remove("is-active");
        document.querySelector("html").classList.remove("is-clipped");
      }
    }
  };
</script>
