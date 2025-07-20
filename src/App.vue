<script setup>
import { ref } from "vue";
import { RouterLink, RouterView } from "vue-router";

const header = ref("Shopping List Application");
</script>

<template>
  <header>
    <nav class="navbar navbar-expand-lg bg-body-tertiary">
      <div class="container-fluid">
        <RouterLink class="navbar-brand" to="/">Navbar</RouterLink>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <RouterLink class="nav-link active" aria-current="page" to="/">Home</RouterLink>
            </li>
            <li class="nav-item">
              <RouterLink class="nav-link" to="/about">About</RouterLink>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </header>

  <!-- <h1>{{ message.toLocaleUpperCase() }}</h1>

  <h1>{{ message ? message : "Welcome" }}</h1>
  <h1>{{ message || "Welcome" }}</h1> -->

  <h1>{{ header }}</h1>

  <!-- <RouterView /> -->
</template>

<style scoped></style>
