<script setup>
import { ref, computed, watch } from "vue";
import HeaderSection from "./components/HeaderSection.vue";
import CourseCard from "./components/CourseCard.vue";
import CartPanel from "./components/CartPanel.vue";

const courses = ref([
  {
    id: 1,
    title: "Italian Pasta Mastery",
    chef: "Chef Marco",
    price: 499,
    soldOut: false,
    image: "images/pasta.jpg",
  },
  {
    id: 2,
    title: "French Pastry Secrets",
    chef: "Chef Claire",
    price: 699,
    soldOut: false,
    image: "images/pastry.jpg",
  },
  {
    id: 3,
    title: "Sushi Fundamentals",
    chef: "Chef Kenji",
    price: 899,
    soldOut: true,
    image: "images/sushi.jpg",
  },
  {
    id: 4,
    title: "South African Braai Skills",
    chef: "Chef Themba",
    price: 399,
    soldOut: false,
    image: "images/braai.jpg",
  },
  {
    id: 5,
    title: "Dessert Artistry",
    chef: "Chef Sofia",
    price: 749,
    soldOut: false,
    image: "images/desert.jpg",
  },
]);

const cart = ref(JSON.parse(localStorage.getItem("cart")) || []);

watch(
  cart,
  (newCart) => {
    localStorage.setItem("cart", JSON.stringify(newCart));
  },
  { deep: true },
);

const couponCode = ref("");
const discountApplied = ref(false);

function addToCart(course) {
  const existing = cart.value.find((item) => item.id === course.id);

  if (existing) {
    existing.quantity++;
  } else {
    cart.value.push({
      ...course,
      quantity: 1,
    });
  }
}

function decreaseQuantity(id) {
  const item = cart.value.find((item) => item.id === id);
  if (!item) return;

  if (item.quantity > 1) {
    item.quantity--;
  } else {
    removeItem(id);
  }
}

function removeItem(id) {
  cart.value = cart.value.filter((item) => item.id !== id);
}

function clearCart() {
  cart.value = [];
  discountApplied.value = false;
}

function applyCoupon() {
  if (couponCode.value.trim().toUpperCase() === "SAVE10") {
    discountApplied.value = true;
  }
}

const subtotal = computed(() => {
  return cart.value.reduce((sum, item) => sum + item.price * item.quantity, 0);
});

const discount = computed(() => {
  return discountApplied.value ? subtotal.value * 0.1 : 0;
});

const taxableAmount = computed(() => {
  return subtotal.value - discount.value;
});

const tax = computed(() => {
  return taxableAmount.value * 0.15;
});

const grandTotal = computed(() => {
  return taxableAmount.value + tax.value;
});
</script>

<template>
  <HeaderSection />
  <main class="layout">
    <section class="catalogue">
      <h2>Available Courses</h2>

      <div class="course-grid">
        <CourseCard
          v-for="course in courses"
          :key="course.id"
          :course="course"
          @add="addToCart"
        />
      </div>
    </section>

    <CartPanel
      :cart="cart"
      :subtotal="subtotal"
      :discount="discount"
      :tax="tax"
      :grandTotal="grandTotal"
      :couponCode="couponCode"
      :discountApplied="discountApplied"
      @increase="increaseQuantity"
      @decrease="decreaseQuantity"
      @remove="removeItem"
      @applyCoupon="applyCoupon"
      @clear="clearCart"
      @update:couponCode="couponCode = $event"
    />
  </main>
</template>
