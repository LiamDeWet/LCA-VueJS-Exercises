<template>
  <div
    class="card"
    :class="{
      featured: ticket.featured,
      bronze: ticket.name === 'Bronze',
      silver: ticket.name === 'Silver',
      gold: ticket.name === 'Gold',
    }"
  >
    <div v-if="ticket.featured" class="badge">MOST POPULAR</div>

    <h2>{{ ticket.name }}</h2>

    <div class="price">R{{ ticket.price }}</div>

    <p class="description">
      {{ ticket.description }}
    </p>

    <ul>
      <li v-for="benefit in ticket.benefits" :key="benefit">✓ {{ benefit }}</li>
    </ul>

    <button class="fav-btn" @click="toggleFavourite">
      {{ ticket.favourite ? "❤️ Favourited" : "🤍 Favourite" }}
    </button>

    <button class="cta" @click="notifyTicket">
      {{ ticket.notified ? "Notification Requested" : "Notify Me" }}
    </button>
  </div>
</template>

<script setup>
const props = defineProps({
  ticket: Object,
});

const emit = defineEmits(["toggle", "notify"]);

function notifyTicket() {
  emit("notify", props.ticket);
}
function toggleFavourite() {
  emit("toggle", props.ticket);
}
</script>

<style scoped>
.card {
  background: #fffcf7;
  border-radius: 16px;
  padding: 25px;
  position: relative;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08);
  transition: all 0.25s ease;
}

.card:hover {
  transform: translateY(-8px);
}

.bronze {
  border-top: 6px solid #a97142;
}

.silver {
  border-top: 6px solid #b8c0c7;
}

.gold {
  border-top: 6px solid #d4a24c;
}

.featured {
  background: linear-gradient(135deg, #fff8e8, #fff1cc);

  border: 3px solid #d4a24c;

  transform: scale(1.04);
}

.badge {
  position: absolute;
  top: -15px;
  right: 15px;
  background: #d4a24c;
  color: white;
  padding: 8px 16px;
  border-radius: 25px;
  font-size: 0.8rem;
  font-weight: bold;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15);
}

.price {
  font-size: 2rem;
  font-weight: bold;
  color: #c76d3a;
  margin: 15px 0;
}

.description {
  margin-bottom: 15px;
}

ul {
  list-style: none;
  margin-bottom: 20px;
}

li {
  margin-bottom: 8px;
}

.fav-btn {
  width: 100%;
  padding: 12px;

  border: none;

  background: #24323f;
  color: white;

  border-radius: 8px;

  cursor: pointer;

  margin-bottom: 10px;
}

.cta {
  width: 100%;
  padding: 12px;

  border: none;

  background: #c76d3a;
  color: white;

  border-radius: 8px;

  cursor: pointer;
}
</style>
