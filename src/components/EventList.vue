<template>
  <section class="grid grid-cols-2 gap-8">
    <template v-if="!loading">
      <EventCard
        v-for="event in events"
        :Key="event.id"
        :title="event.title"
        :when="event.date"
        :description="event.description"
        @register="$emit('register', event)"
      />
    </template>
    <template v-else>
      <LoadingEventCard v-for="i in 4" :key="i" />
    </template>
  </section>
</template>

<script setup>
import EventCard from '@/components/EventCard.vue';
import LoadingEventCard from '@/components/LoadingEventCard.vue';

import { API_URL } from '@/utils/config.js';
import { onMounted, ref } from 'vue';

defineProps({
  bookings: Array,
  bookingsLoading: Boolean
});

defineEmits(['register']);

const events = ref([]);
const loading = ref(true);

const fetchEvents = async () => {
  try {
    const res = await fetch(`${API_URL}/events`);
    events.value = await res.json();
  } finally {
    loading.value = false;
  }
};

onMounted(() => {
  fetchEvents();
});
</script>
