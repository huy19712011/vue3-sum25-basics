<script setup>
import { ref } from "vue";

// === state ===
const books = ref([
  { id: 1, title: "Book 1", description: "Description 1", price: 11 },
  { id: 2, title: "Book 2", description: "Description 2", price: 12 },
  { id: 3, title: "Book 3", description: "Description 3", price: 13 },
]);

const form = ref({
  id: null,
  title: "",
  description: "",
  price: null,
});

const isEditing = ref(false);

// === methods ===
function handleSubmit() {
  if (isEditing.value) {
    updateBook();
  } else {
    addBook();
  }
}

function addBook() {
  const newId = books.value.length + 1;

  books.value.push({
    id: newId,
    title: form.value.title,
    description: form.value.description,
    price: form.value.price,
  });

  resetForm();
}

function editBook(book) {
  isEditing.value = true;
  form.value = { ...book }; // load into form
}

function updateBook() {
  const index = books.value.findIndex((s) => s.id === form.value.id);
  books.value[index] = { ...form.value };

  resetForm();
  isEditing.value = false;
}

function deleteBook(id) {
  books.value = books.value.filter((s) => s.id !== id);
}

function cancelEdit() {
  resetForm();
  isEditing.value = false;
}

function resetForm() {
  form.value = { id: null, title: "", description: "", price: null };
}
</script>

<template>
  <div class="container">
    <h2>Book Management</h2>

    <!-- Form -->
    <form @submit.prevent="handleSubmit" class="form">
      <input v-model="form.title" placeholder="Title" required />
      <input v-model="form.description" placeholder="Description" required />
      <input v-model="form.price" placeholder="Price" required />

      <button type="submit">
        {{ isEditing ? "Update Book" : "Add Book" }}
      </button>
      <button v-if="isEditing" type="button" @click="cancelEdit">Cancel</button>
    </form>

    <!-- Table -->
    <table border="1" cellpadding="6" style="width: 100%">
      <thead>
        <tr>
          <th>Id</th>
          <th>Title</th>
          <th>Description</th>
          <th>Price</th>
          <th>Actions</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="book in books" :key="book.id">
          <td>{{ book.id }}</td>
          <td>{{ book.title }}</td>
          <td>{{ book.description }}</td>
          <td>{{ book.price }}</td>
          <td>
            <button @click="editBook(book)">Edit</button>
            <button @click="deleteBook(book.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
.container {
  width: 600px;
  margin: auto;
}
form {
  margin-bottom: 20px;
  display: flex;
  flex-direction: column;
  gap: 8px;
  flex-wrap: wrap;
}
input {
  padding: 6px;
}
button {
  padding: 6px 32px;
}
</style>
