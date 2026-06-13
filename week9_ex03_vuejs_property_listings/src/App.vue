<script setup>
import { ref, computed, watch } from "vue";
import HeaderSection from "./components/HeaderSection.vue";
import PropertyCard from "./components/PropertyCard.vue";

const searchTerm = ref("");
const sortOrder = ref("low");
const maxPrice = ref(7000);

const properties = ref([
  {
    id: 1,
    title: "Luxury Sea Point Apartment",
    location: "Sea Point",
    price: 2500,
    type: "Apartment",
    available: true,
    bookmarked: false,
    image: "images/seapoint.jpg",
  },
  {
    id: 2,
    title: "Camps Bay Villa",
    location: "Camps Bay",
    price: 5500,
    type: "Villa",
    available: true,
    bookmarked: false,
    image: "images/villa.jpg",
  },
  {
    id: 3,
    title: "City Loft",
    location: "Cape+Town+CBD",
    price: 1800,
    type: "Loft",
    available: false,
    bookmarked: false,
    image: "images/loft.jpg",
  },
  {
    id: 4,
    title: "Blouberg Beach House",
    location: "Blouberg",
    price: 4200,
    type: "House",
    available: true,
    bookmarked: false,
    image: "images/beachhouse.jpg",
  },
  {
    id: 5,
    title: "Waterfront Penthouse",
    location: "V&A Waterfront",
    price: 6800,
    type: "Penthouse",
    available: true,
    bookmarked: false,
    image: "images/V&A.jpg",
  },
  {
    id: 6,
    title: "Woodstock Studio",
    location: "Woodstock",
    price: 1400,
    type: "Studio",
    available: false,
    bookmarked: false,
    image: "images/studio.jpg",
  },
]);

const savedBookmarks = JSON.parse(localStorage.getItem("bookmarks")) || [];

properties.value.forEach((property) => {
  property.bookmarked = savedBookmarks.includes(property.id);
});

watch(
  properties,
  () => {
    const bookmarks = properties.value
      .filter((property) => property.bookmarked)
      .map((property) => property.id);

    localStorage.setItem("bookmarks", JSON.stringify(bookmarks));
  },
  { deep: true },
);

function toggleBookmark(property) {
  property.bookmarked = !property.bookmarked;
}

const filteredProperties = computed(() => {
  let result = properties.value.filter(
    (property) =>
      (property.title.toLowerCase().includes(searchTerm.value.toLowerCase()) ||
        property.location
          .toLowerCase()
          .includes(searchTerm.value.toLowerCase())) &&
      property.price <= maxPrice.value,
  );

  result.sort((a, b) =>
    sortOrder.value === "low" ? a.price - b.price : b.price - a.price,
  );

  return result;
});

const bookmarkedCount = computed(
  () => properties.value.filter((p) => p.bookmarked).length,
);
</script>

<template>
  <HeaderSection
    :totalProperties="filteredProperties.length"
    :bookmarkedCount="bookmarkedCount"
  />

  <section class="controls">
    <input
      v-model="searchTerm"
      class="search"
      placeholder="Search by title or location..."
    />

    <select v-model="sortOrder">
      <option value="low">Price: Low → High</option>
      <option value="high">Price: High → Low</option>
    </select>

    <div class="slider-group">
      <label> Max Price: R{{ maxPrice }} </label>

      <input type="range" min="1000" max="7000" step="100" v-model="maxPrice" />
    </div>
  </section>

  <TransitionGroup name="properties" tag="section" class="property-grid">
    <PropertyCard
      v-for="property in filteredProperties"
      :key="property.id"
      :property="property"
      @bookmark="toggleBookmark"
    />
  </TransitionGroup>
</template>
