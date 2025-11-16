<script setup>
import { ref } from "vue";

// === state ===
const students = ref([
  { id: 1, name: "Alice", email: "alice@mail.com", phone: "0123456789" },
  { id: 2, name: "Bob", email: "bob@mail.com", phone: "0987654321" },
]);

const form = ref({
  id: null,
  name: "",
  email: "",
  phone: "",
});

const isEditing = ref(false);

// === methods ===
function handleSubmit() {
  if (isEditing.value) {
    updateStudent();
  } else {
    addStudent();
  }
}

function addStudent() {
  const newId = students.value.length + 1;

  students.value.push({
    id: newId,
    name: form.value.name,
    email: form.value.email,
    phone: form.value.phone,
  });

  resetForm();
}

function editStudent(student) {
  isEditing.value = true;
  form.value = { ...student }; // load into form
}

function updateStudent() {
  const index = students.value.findIndex((s) => s.id === form.value.id);
  students.value[index] = { ...form.value };

  resetForm();
  isEditing.value = false;
}

function deleteStudent(id) {
  students.value = students.value.filter((s) => s.id !== id);
}

function cancelEdit() {
  resetForm();
  isEditing.value = false;
}

function resetForm() {
  form.value = { id: null, name: "", email: "", phone: "" };
}
</script>

<template>
  <div class="container">
    <h2>Student Management</h2>

    <!-- Form -->
    <form @submit.prevent="handleSubmit" class="form">
      <input v-model="form.name" placeholder="Name" required />
      <input v-model="form.email" placeholder="Email" required />
      <input v-model="form.phone" placeholder="Phone" required />

      <button type="submit">
        {{ isEditing ? "Update Student" : "Add Student" }}
      </button>
      <button v-if="isEditing" type="button" @click="cancelEdit">Cancel</button>
    </form>

    <!-- Table -->
    <table border="1" cellpadding="6" style="width: 100%">
      <thead>
        <tr>
          <th>ID</th>
          <th>Name</th>
          <th>Email</th>
          <th>Phone</th>
          <th>Actions</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="stu in students" :key="stu.id">
          <td>{{ stu.id }}</td>
          <td>{{ stu.name }}</td>
          <td>{{ stu.email }}</td>
          <td>{{ stu.phone }}</td>
          <td>
            <button @click="editStudent(stu)">Edit</button>
            <button @click="deleteStudent(stu.id)">Delete</button>
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
