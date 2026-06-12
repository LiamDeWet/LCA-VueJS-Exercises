<script setup>
import { ref, computed } from "vue";
import HeaderSection from "./components/HeaderSection.vue";
import TicketCard from "./components/TicketCard.vue";

const sortOrder = ref("low");
const tickets = ref([
  {
    id: 1,
    name: "Bronze",
    price: 299,
    description: "Single day access.",
    benefits: ["Festival Entry", "Live Music", "Food Market Access"],
    featured: false,
    favourite: false,
    notified: false,
  },

  {
    id: 2,
    name: "Student Pass",
    price: 199,
    description: "Discounted student ticket.",
    benefits: ["Festival Entry", "Live Music"],
    featured: false,
    favourite: false,
    notified: false,
  },

  {
    id: 3,
    name: "Family Pass",
    price: 799,
    description: "Perfect for families.",
    benefits: ["4 Entries", "Kids Zone Access", "Live Music"],
    featured: false,
    favourite: false,
    notified: false,
  },

  {
    id: 4,
    name: "Weekend Pass",
    price: 599,
    description: "Access both festival days.",
    benefits: ["2-Day Entry", "Music Access", "Food Market"],
    featured: false,
    favourite: false,
    notified: false,
  },

  {
    id: 5,
    name: "Silver VIP",
    price: 999,
    description: "Priority festival experience.",
    benefits: ["Priority Entry", "VIP Seating", "Festival Entry"],
    featured: true,
    favourite: false,
    notified: false,
  },

  {
    id: 6,
    name: "Gold VIP",
    price: 1499,
    description: "Ultimate Food Fest package.",
    benefits: [
      "VIP Lounge",
      "Chef Meet & Greet",
      "Priority Entry",
      "Reserved Seating",
    ],
    featured: true,
    favourite: false,
    notified: false,
  },

  {
    id: 7,
    name: "Vendor Pass",
    price: 1299,
    description: "For participating vendors.",
    benefits: ["Vendor Area", "2 Staff Entries", "Setup Access"],
    featured: false,
    favourite: false,
    notified: false,
  },
]);

function notifyMe(ticket) {
  ticket.notified = !ticket.notified;
}

function toggleFavourite(ticket) {
  ticket.favourite = !ticket.favourite;
}
const favouriteCount = computed(() => {
  return tickets.value.filter((ticket) => ticket.favourite).length;
});

const sortedTickets = computed(() => {
  return [...tickets.value].sort((a, b) => {
    return sortOrder.value === "low" ? a.price - b.price : b.price - a.price;
  });
});

const featuredTickets = computed(() =>
  tickets.value.filter((ticket) => ticket.featured),
);

const regularTickets = computed(() =>
  tickets.value.filter((ticket) => !ticket.featured),
);
</script>

<template>
  <HeaderSection :favouriteCount="favouriteCount" />

  <section class="controls">
    <label>
      Sort By:
      <select v-model="sortOrder">
        <option value="low">Lowest Price First</option>
        <option value="high">Highest Price First</option>
      </select>
    </label>
  </section>

  <section class="featured-section">
    <h2>⭐ Featured Experiences</h2>

    <div class="featured-grid">
      <TicketCard
        v-for="ticket in featuredTickets"
        :key="ticket.id"
        :ticket="ticket"
        @toggle="toggleFavourite"
        @notify="notifyMe"
      />
    </div>
  </section>

  <section class="tickets-section">
    <h2>🎟️ All Ticket Options</h2>

    <div class="ticket-grid">
      <TicketCard
        v-for="ticket in regularTickets"
        :key="ticket.id"
        :ticket="ticket"
        @toggle="toggleFavourite"
        @notify="notifyMe"
      />
    </div>
  </section>
</template>
