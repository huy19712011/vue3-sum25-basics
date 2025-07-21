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

const newItemHighPriority = ref(false);

const saveItem = () => {
  items.value.push({ id: items.value.length + 1, label: newItem.value });
  newItem.value = "";
};
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

  <h1>{{ header }}</h1>
  <form class="add-item-form" v-on:submit.prevent="saveItem">
    <input v-model.trim="newItem" type="text" placeholder="Add an Item" />
    <!-- {{ newItem }} -->

    <label>
      <input type="checkbox" v-model="newItemHighPriority" />
      High Priority
    </label>
    <button class="btn btn-primary">Save Item</button>
  </form>
  <ul>
    <!-- <li v-for="{ id, label } in items" v-bind:key="id">{{ label }}</li> -->
    <li v-for="({ id, label }, index) in items" v-bind:key="id">{{ index }}: {{ label }}</li>
  </ul>

  <!-- <RouterView /> -->
</template>

<style scoped></style>
