<template>
  <header class="hero">
    <h1>FlexZone Fitness</h1>

    <p>Manage gym classes and schedules with ease.</p>

    <div class="stats">
      <span> Classes: {{ totalSessions }} </span>

      <span v-if="nextSession">
        Next:
        {{ nextSession.name }} -
        {{ nextSession.date }}
        {{ nextSession.time }}
      </span>
    </div>
  </header>
</template>

<script setup>
defineProps({
  totalSessions: Number,
  nextSession: Object,
});
</script>

<style scoped>
.hero {
  min-height: 350px;

  background:
    linear-gradient(rgba(0, 0, 0, 0.55), rgba(0, 0, 0, 0.55)),
    url("images/sport.jpg");

  background-size: cover;
  background-position: center;

  color: white;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  text-align: center;

  padding: 60px 20px;
}

.hero h1 {
  font-size: 3.2rem;
  margin-bottom: 15px;
}

.hero p {
  max-width: 700px;
  font-size: 1.2rem;
}

.stats {
  margin-top: 25px;

  display: flex;
  gap: 20px;
  flex-wrap: wrap;
}

.stats span {
  background: rgba(255, 255, 255, 0.15);

  backdrop-filter: blur(10px);

  padding: 12px 20px;

  border-radius: 12px;

  font-weight: bold;
}
</style>
