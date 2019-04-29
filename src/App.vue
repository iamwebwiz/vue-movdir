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
                <button class="button is-info">Add Movie</button>
              </div>
            </div>
          </div>
          <hr>
          <Home/>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
  import Home from "@/views/Home";

  export default {
    components: {
      Home
    }
  };
</script>
