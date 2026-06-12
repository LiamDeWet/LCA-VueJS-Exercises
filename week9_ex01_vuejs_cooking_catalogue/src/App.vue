<script setup>
import { ref, computed } from "vue";
import HeaderBar from "./components/HeaderBar.vue";
import CourseCard from "./components/CourseCard.vue";

const wishlist = ref([]);

const courses = ref([
  {
    id: 1,
    title: "Italian Pasta Mastery",
    chef: "Chef Marco",
    level: "Beginner",
    price: 499,
    available: true,
    saved: false,
  },
  {
    id: 2,
    title: "French Pastry Secrets",
    chef: "Chef Claire",
    level: "Intermediate",
    price: 699,
    available: true,
    saved: false,
  },
  {
    id: 3,
    title: "Sushi Fundamentals",
    chef: "Chef Kenji",
    level: "Advanced",
    price: 899,
    available: false,
    saved: false,
  },
  {
    id: 4,
    title: "South African Braai Skills",
    chef: "Chef Themba",
    level: "Beginner",
    price: 399,
    available: true,
    saved: false,
  },
  {
    id: 5,
    title: "Dessert Artistry",
    chef: "Chef Sofia",
    level: "Intermediate",
    price: 749,
    available: false,
    saved: false,
  },
]);

const showAvailableOnly = ref(false);

const filteredCourses = computed(() => {
  if (showAvailableOnly.value) {
    return courses.value.filter((course) => course.available);
  }
  return courses.value;
});

function addToWishlist(course) {
  if (!course.saved) {
    course.saved = true;
    wishlist.value.push(course);
  }
}

function removeFromWishlist(course) {
  course.saved = false;

  wishlist.value = wishlist.value.filter((item) => item.id !== course.id);
}
</script>

<template>
  <HeaderBar :wishlistCount="wishlist.length" />

  <main class="layout">
    <section class="catalogue">
      <h2>Available Cooking Courses</h2>

      <label class="filter">
        <input type="checkbox" v-model="showAvailableOnly" />
        Show Available Only
      </label>

      <div class="grid">
        <CourseCard
          v-for="course in filteredCourses"
          :key="course.id"
          :course="course"
          @save="addToWishlist"
        />
      </div>
    </section>

    <aside class="wishlist-panel">
      <h2>My Wishlist</h2>

      <p v-if="wishlist.length === 0">No courses saved yet.</p>

      <div v-for="course in wishlist" :key="course.id" class="wishlist-item">
        <h4>{{ course.title }}</h4>
        <p>{{ course.chef }}</p>
        <p>R{{ course.price }}</p>

        <button class="remove-btn" @click="removeFromWishlist(course)">
          Remove
        </button>
      </div>
    </aside>
  </main>
</template>
