<template>
  <div id="app">
    <section class="hero">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">Vue Movies CRUD</h1>
          <h2 class="subtitle">Manage Movies in one place</h2>
          <hr>
          <Home/>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
  import Home from "@/views/Home.vue";

  export default {
    components: {
      Home
    }
  };
</script>
