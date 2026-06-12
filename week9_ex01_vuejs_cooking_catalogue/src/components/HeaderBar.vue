<template>
  <header class="header">
    <h1>🍳 Cooking Masterclass</h1>

    <div class="wishlist">❤️ Wishlist: {{ wishlistCount }}</div>
  </header>
</template>

<script setup>
defineProps({
  wishlistCount: Number,
});
</script>

<style scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px 30px;
  background: #2f3a44;
  color: white;
  box-shadow: 0 3px 12px rgba(0, 0, 0, 0.15);
}

.wishlist {
  font-weight: bold;
  font-size: 1.1rem;
}
</style>
