<template>
  <article class="card">
    <div v-if="!property.available" class="badge">NOT AVAILABLE</div>

    <div class="image-wrapper">
      <img :src="property.image" :alt="property.title" />
    </div>

    <div class="content">
      <h2>{{ property.title }}</h2>

      <p class="location">📍 {{ property.location }}</p>

      <p class="type">
        {{ property.type }}
      </p>

      <div class="price">R{{ property.price }}/night</div>

      <button class="bookmark" @click="toggleBookmark">
        {{ property.bookmarked ? "❤️ Bookmarked" : "🤍 Bookmark" }}
      </button>
    </div>
  </article>
</template>

<script setup>
const props = defineProps({
  property: Object,
});

const emit = defineEmits(["bookmark"]);

function toggleBookmark() {
  emit("bookmark", props.property);
}
</script>

<style scoped>
.card {
  background: white;
  border-radius: 16px;
  overflow: hidden;
  box-shadow: 0 4px 14px rgba(0, 0, 0, 0.08);
  transition: 0.25s;
  position: relative;
  display: flex;
  flex-direction: column;
}

.card:hover {
  transform: translateY(-6px);
}

.image-wrapper {
  width: 100%;
  aspect-ratio: 16/10;
  overflow: hidden;
}

.image-wrapper img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.content {
  padding: 18px;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}

.location {
  margin-top: 10px;
}

.type {
  color: #666;
  margin-top: 5px;
}

.price {
  font-size: 1.3rem;
  font-weight: bold;
  color: #c76d3a;
  margin: 15px 0;
}

.bookmark {
  margin-top: auto;
  width: 100%;
  padding: 12px;
  border: none;
  background: #24323f;
  color: white;
  border-radius: 8px;
  cursor: pointer;
}

.badge {
  position: absolute;
  top: 12px;
  right: 12px;
  background: #b54747;
  color: white;
  padding: 8px 12px;
  border-radius: 20px;
  z-index: 2;
  font-size: 0.8rem;
  font-weight: bold;
}
</style>
