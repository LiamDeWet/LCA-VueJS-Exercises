<script setup>
import { ref } from "vue";

const emit = defineEmits(["add-session"]);

const name = ref("");
const coach = ref("");
const date = ref("");
const time = ref("");
const capacity = ref("");
const error = ref("");

function submitForm() {
  error.value = "";

  if (
    !name.value ||
    !coach.value ||
    !date.value ||
    !time.value ||
    !capacity.value
  ) {
    error.value = "All fields are required.";
    return;
  }

  if (capacity.value <= 0) {
    error.value = "Capacity must be greater than 0. ";
    return;
  }

  emit("add-session", {
    name: name.value,
    coach: coach.value,
    date: date.value,
    time: time.value,
    capacity: Number(capacity.value),
  });

  name.value = "";
  coach.value = "";
  date.value = "";
  time.value = "";
  capacity.value = "";
}
</script>

<template>
  <section class="form-card">
    <h2>Add New Class</h2>

    <p v-if="error" class="error">
      {{ error }}
    </p>

    <div class="form-grid">
      <input v-model="name" placeholder="Class Name" />

      <input v-model="coach" placeholder="Coach Name" />

      <input type="date" v-model="date" />

      <input type="time" v-model="time" />

      <input type="number" min="1" v-model="capacity" placeholder="Capacity" />
    </div>

    <button type="button" @click="submitForm">Add Session</button>
  </section>
</template>

<style scoped>
.form-card {
  background: white;
  padding: 25px;
  border-radius: 16px;
}

.form-grid {
  display: grid;
  gap: 12px;
  margin: 15px;
}

.error {
  color: red;
  margin-top: 10px;
}

.form-card {
  background: white;

  padding: 30px;

  border-radius: 20px;

  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.08);

  margin-bottom: 40px;
}

.form-card h2 {
  margin-bottom: 20px;
}

.form-grid {
  display: grid;

  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));

  gap: 15px;
}

.form-grid input {
  padding: 14px;

  border: 1px solid #ddd;

  border-radius: 10px;
}

button {
  margin-top: 20px;

  background: #2563eb;

  color: white;

  border: none;

  padding: 14px 24px;

  border-radius: 10px;

  cursor: pointer;

  transition: 0.3s;
}

button:hover {
  transform: translateY(-2px);
}
</style>
