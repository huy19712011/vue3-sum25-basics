<script setup>
import { ref, computed } from "vue";
import { RouterLink, RouterView } from "vue-router";

const header = ref("Shopping List Application");

const items = ref([
  { id: 1, label: "10 product-1", purchased: true, highPriority: false },
  { id: 2, label: "2 product-2", purchased: true, highPriority: false },
  { id: 3, label: "3 product-3", purchased: false, highPriority: true },
  { id: 4, label: "4 product-4", purchased: false, highPriority: true },
]);

const newItem = ref("");

const newItemHighPriority = ref(false);

const saveItem = () => {
  items.value.push({
    id: items.value.length + 1,
    label: newItem.value,
    highPriority: newItemHighPriority.value,
  });
  newItem.value = "";
  newItemHighPriority.value = false;
};

const editing = ref(false);

const doEdit = (e) => {
  editing.value = e;
  newItem.value = "";
};

const togglePurchased = (item) => {
  item.purchased = !item.purchased;
};

const characterCount = computed(() => {
  return newItem.value.length;
});

const reversedItems = computed(() => {
  return [...items.value].reverse();
});
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
            <li class="nav-item">
              <RouterLink class="nav-link" to="/student">Student</RouterLink>
            </li>
            <li class="nav-item">
              <RouterLink class="nav-link" to="/book">Book</RouterLink>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </header>

  <RouterView />
</template>

<style scoped></style>
