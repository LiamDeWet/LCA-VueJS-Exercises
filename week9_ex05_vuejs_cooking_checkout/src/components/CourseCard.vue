<template>
  <article class="card">
    <div v-if="course.soldOut" class="badge">SOLD OUT</div>

    <img :src="course.image" :alt="course.title" />

    <div class="content">
      <h3>{{ course.title }}</h3>
      <p>{{ course.chef }}</p>
      <div class="price">R{{ course.price }}</div>

      <button :disabled="course.soldOut" @click="emit('add', course)">
        Add To Cart
      </button>
    </div>
  </article>
</template>

<script setup>
defineProps({
  course: Object,
});

const emit = defineEmits(["add"]);
</script>
