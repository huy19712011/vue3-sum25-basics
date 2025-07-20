<script setup>
import { ref } from "vue";
import { RouterLink, RouterView } from "vue-router";

const header = ref("Shopping List Application");

const items = ref([
  { id: 1, label: "10 product-1" },
  { id: 2, label: "2 product-2" },
  { id: 3, label: "3 product-3" },
  { id: 4, label: "4 product-4" },
]);

const newItem = ref("");

const newItemPriority = ref("low");

const newItemHighPriority = ref(false);

const iceCreamFlavors = ref([]);
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
  <input v-model.trim="newItem" type="text" placeholder="Add an Item" />
  <!-- {{ newItem }} -->

  <!-- <label>
    Priority:
    <input type="radio" v-model="newItemPriority" value="low" />
    Low
  </label>
  <label>
    <input type="radio" v-model="newItemPriority" value="high" />
    High
  </label> -->

  <!-- <label>
    Priority:
    <select v-model="newItemPriority">
      <option value="low">Low</option>
      <option value="high">High</option>
    </select>
  </label>
  <br />
  {{ newItemPriority }} -->

  <label>
    <input type="checkbox" v-model="newItemHighPriority" />
    High Priority
  </label>
  <br />
  {{ newItemHighPriority }}

  <br />
  <label> <input type="checkbox" value="vanilla" v-model="iceCreamFlavors" /> Vanilla </label>
  <label> <input type="checkbox" value="chocolate" v-model="iceCreamFlavors" /> Chocolate </label>
  <label> <input type="checkbox" value="strawberry" v-model="iceCreamFlavors" /> Strawberry </label
  ><br />
  {{ iceCreamFlavors }}

  <ul>
    <!-- <li v-for="{ id, label } in items" v-bind:key="id">{{ label }}</li> -->
    <li v-for="({ id, label }, index) in items" v-bind:key="id">{{ index }}: {{ label }}</li>
  </ul>

  <!-- <RouterView /> -->
</template>

<style scoped></style>
