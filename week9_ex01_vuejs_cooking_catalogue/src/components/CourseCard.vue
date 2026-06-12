<template>
  <div class="card">
    <h2>{{ course.title }}</h2>

    <p>
      <strong>Chef:</strong>
      {{ course.chef }}
    </p>

    <p>
      <strong>Level:</strong>
      {{ course.level }}
    </p>

    <p class="price">R{{ course.price.toFixed(2) }}</p>

    <p v-if="!course.available" class="sold-out">SOLD OUT</p>

    <button @click="saveCourse" :disabled="!course.available || course.saved">
      {{ course.saved ? "Saved ✓" : "Save Course" }}
    </button>
  </div>
</template>

<script setup>
const props = defineProps({
  course: Object,
});

const emit = defineEmits(["save"]);

function saveCourse() {
  emit("save", props.course);
}
</script>

<style scoped>
.card {
  background: #fffcf7;
  border-radius: 12px;
  padding: 20px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
  transition: all 0.25s ease;
}

.card:hover {
  transform: translateY(-6px);
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.12);
}

.price {
  font-size: 1.2rem;
  font-weight: bold;
  color: #c76d3a;
}

.sold-out {
  color: red;
  font-weight: bold;
  margin-bottom: 10px;
}

button {
  width: 100%;
  padding: 10px;
  border: none;
  background: #c76d3a;
  color: white;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.2s ease;
}

button:hover:not(:disabled) {
  opacity: 0.9;
  background: #a8562a;
}

button:disabled {
  background: gray;
  cursor: not-allowed;
}
</style>
