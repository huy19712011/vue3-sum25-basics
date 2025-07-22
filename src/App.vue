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
          </ul>
        </div>
      </div>
    </nav>
  </header>

  <div class="header">
    <h1>{{ header }}</h1>
    <button v-if="editing" class="btn" @click="doEdit(false)">Cancel</button>
    <button v-else class="btn btn-primary" @click="doEdit(true)">Add Item</button>
  </div>
  <!-- <a v-bind:href="newItem">Dynamic Link</a> -->
  <form class="add-item-form" v-if="editing" v-on:submit.prevent="saveItem">
    <input v-model.trim="newItem" type="text" placeholder="Add an Item" />
    <!-- {{ newItem }} -->

    <label>
      <input type="checkbox" v-model="newItemHighPriority" />
      High Priority
    </label>
    <!-- <button v-bind:disabled="newItem.length < 2" class="btn btn-primary">Save Item</button> -->
    <button :disabled="newItem.length < 2" class="btn btn-primary">Save Item</button>
  </form>
  <p class="counter">{{ characterCount }}/200</p>

  <ul>
    <!-- <li v-for="{ id, label } in items" v-bind:key="id">{{ label }}</li> -->
    <!-- object syntax -->
    <li
      v-for="({ id, label, purchased, highPriority }, index) in reversedItems"
      v-bind:key="id"
      class="static-class"
      :class="{ strikeout: purchased, priority: highPriority }"
      @click="togglePurchased(items[index])"
    >
      {{ index + 1 }}: {{ label }}
    </li>
    <!-- array syntax -->
    <li
      v-for="({ id, label, purchased, highPriority }, index) in items"
      v-bind:key="id"
      class="static-class"
      :class="[purchased ? 'strikeout text-gray' : 'underlined', highPriority ? 'priority' : '']"
    >
      {{ index + 1 }}: {{ label }}
    </li>
    <!-- array + object syntax -->
    <li
      v-for="({ id, label, purchased, highPriority }, index) in items"
      v-bind:key="id"
      class="static-class"
      :class="[{ strikeout: purchased }, { priority: highPriority }]"
    >
      {{ index + 1 }}: {{ label }}
    </li>
  </ul>
  <p v-if="!items.length">Nothing to see here!</p>

  <!-- <RouterView /> -->
</template>

<style scoped></style>
