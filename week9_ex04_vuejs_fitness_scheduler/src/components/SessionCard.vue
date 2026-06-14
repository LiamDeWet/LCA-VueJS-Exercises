<template>
  <article class="card">
    <h3>{{ session.name }}</h3>

    <p>
      Coach:
      {{ session.coach }}
    </p>

    <p>
      {{ session.date }}
    </p>

    <p>
      {{ session.time }}
    </p>

    <p>
      Capacity:
      {{ session.capacity }}
    </p>

    <button class="delete-btn" @click="emit('delete-session', session.id)">
      Delete
    </button>
  </article>
</template>

<script setup>
defineProps({
  session: Object,
});

const emit = defineEmits(["delete-session"]);
</script>

<style scoped>
.card {
  background: white;
  border-radius: 16px;
  padding: 20px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
}

.delete-btn {
  margin-top: 15px;
  width: 100%;
  border: none;
  background: #b54747;
  color: white;
  padding: 10px;
  border-radius: 8px;
  cursor: pointer;
}

.card {
  background: white;

  border-radius: 20px;

  padding: 25px;

  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.08);

  transition: 0.3s;

  border-top: 5px solid #2563eb;
}

.card:hover {
  transform: translateY(-6px);
}

.card h3 {
  margin-bottom: 15px;

  color: #2563eb;
}

.card p {
  margin-bottom: 10px;
}

.delete-btn {
  margin-top: 20px;

  width: 100%;

  padding: 12px;

  border: none;

  background: #dc2626;

  color: white;

  border-radius: 10px;

  cursor: pointer;
}
</style>
