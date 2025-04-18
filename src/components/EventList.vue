<template>
  <template v-if="error">
    <SectionCard>
      <div class="space-y-4 items-center flex flex-col">
        <div class="text-red-500">Could not load events at the moment. Please try again.</div>
        <ReadButton @click="fetchEvents">Retry now</ReadButton>
      </div>
    </SectionCard>
  </template>
  <template v-else>
    <section class="grid grid-cols-1 lg:grid-cols-2 gap-8">
      <template v-if="!loading">
        <template v-if="events.length">
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
          <div class="col-span-2 text-center text-gray-500">No events yet.</div>
        </template>
      </template>
      <template v-else>
        <LoadingEventCard v-for="i in 4" :key="i" />
      </template>
    </section>
  </template>
</template>

<script setup>
import EventCard from '@/components/EventCard.vue';
import LoadingEventCard from '@/components/LoadingEventCard.vue';
import ReadButton from '@/components/ReadButton.vue';

import SectionCard from '@/components/SectionCard.vue';
import { API_URL } from '@/utils/config.js';
import { onMounted, ref } from 'vue';

defineProps({
  bookings: Array,
  bookingsLoading: Boolean
});

defineEmits(['register']);

const events = ref([]);
const loading = ref(false);
const error = ref(null);

const fetchEvents = async () => {
  loading.value = true;
  error.value = null;
  try {
    const res = await fetch(`${API_URL}/events`);
    events.value = await res.json();
  } catch (err) {
    error.value = err;
  } finally {
    loading.value = false;
  }
};

onMounted(() => {
  fetchEvents();
});
</script>
