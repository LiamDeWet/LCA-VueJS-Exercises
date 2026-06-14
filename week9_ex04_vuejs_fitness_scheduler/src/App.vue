<script setup>
import { ref, computed, watch } from "vue";
import HeaderSection from "./components/HeaderSection.vue";
import AddSessionForm from "./components/AddSessionForm.vue";
import SessionCard from "./components/SessionCard.vue";

const searchCoach = ref("");

const savedSessions = JSON.parse(localStorage.getItem("sessions")) || [];

const sessions = ref(savedSessions);

watch(
  sessions,
  (newSessions) => {
    localStorage.setItem("sessions", JSON.stringify(newSessions));
  },
  { deep: true },
);

function addSession(session) {
  sessions.value.push({
    ...session,
    id: Date.now(),
  });
}

function deleteSession(id) {
  sessions.value = sessions.value.filter((session) => session.id !== id);
}

const filteredSessions = computed(() => {
  return sessions.value.filter((session) =>
    session.coach.toLowerCase().includes(searchCoach.value.toLowerCase()),
  );
});

const totalSessions = computed(() => {
  return sessions.value.length;
});

const nextSession = computed(() => {
  const futureSessions = sessions.value
    .filter(
      (session) => new Date(`${session.date}T${session.time}`) > new Date(),
    )
    .sort(
      (a, b) =>
        new Date(`${a.date}T${a.time}`) - new Date(`${b.date}T${b.time}`),
    );

  return futureSessions[0] || null;
});
</script>

<template>
  <HeaderSection :totalSessions="totalSessions" :nextSession="nextSession" />

  <main class="container">
    <AddSessionForm @add-session="addSession" />

    <div class="toolbar">
      <input v-model="searchCoach" placeholder="Search By Coach..." />
    </div>

    <div v-if="!filteredSessions.length" class="empty-state">
      No Sessions scheduled.
    </div>

    <TransitionGroup name="sessions" tag="div" class="session-grid">
      <SessionCard
        v-for="session in filteredSessions"
        :key="session.id"
        :session="session"
        @delete-session="deleteSession"
      />
    </TransitionGroup>
  </main>
</template>
