<template>
  <header class="hero">
    <h1>Cooking Masterclass</h1>

    <p>Discover world-class culinary experiences and master new skills.</p>
  </header>
</template>

<style scoped>
.hero {
  min-height: 320px;
  background:
    linear-gradient(rgba(0, 0, 0, 0.55), rgba(0, 0, 0, 0.55)),
    url("images/cooking2.jpg");
  background-size: cover;
  background-position: center;
  color: white;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.hero h1 {
  font-size: 3rem;
}
</style>
