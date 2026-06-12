<template>
  <header class="hero">
    <h1>Cape Town Food Fest 2026</h1>

    <p>
      Experience a weekend of world-class food, live music, and unforgettable
      memories.
    </p>

    <div class="favourites">❤️ Favourite Tickets: {{ favouriteCount }}</div>
  </header>
</template>

<script setup>
defineProps({
  favouriteCount: Number,
});
</script>

<style scoped>
.hero {
  background: #800020;
  color: white;
  text-align: center;
  padding: 60px 20px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.15);
}

.hero h1 {
  font-size: 3rem;
  margin-bottom: 15px;
}

.hero p {
  max-width: 700px;
  margin: auto;
  line-height: 1.6;
}

.favourites {
  margin-top: 20px;
  font-size: 1.1rem;
  font-weight: bold;
}
</style>
