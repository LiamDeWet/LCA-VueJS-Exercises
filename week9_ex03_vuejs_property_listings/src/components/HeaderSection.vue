<template>
  <header class="hero">
    <h1>Homes & Beyond</h1>

    <p>Discover premium short-term rentals across Cape Town.</p>

    <div class="stats">
      <span>🏠 {{ totalProperties }} Properties</span>
      <span>❤️ {{ bookmarkedCount }} Saved</span>
    </div>
  </header>
</template>

<script setup>
defineProps({
  totalProperties: Number,
  bookmarkedCount: Number,
});
</script>

<style scoped>
.hero {
  background: #24323f;
  color: white;
  text-align: center;
  padding: 60px 20px;
}

.stats {
  margin-top: 20px;
  display: flex;
  justify-content: center;
  gap: 25px;
  font-weight: bold;
}

@media (max-width: 600px) {
  .stats {
    flex-direction: column;
    gap: 10px;
  }
}
</style>
