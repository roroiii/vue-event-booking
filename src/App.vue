<template>
  <main class="container mx-auto my-8 space-y-8">
    <h1 class="text-4xl font-medium">Event Booking</h1>
    <h2 class="text-2xl font-medium">All Events</h2>
    <section class="grid grid-cols-2 gap-8">
      <template v-if="!eventsLoading">
        <EventCard
          v-for="event in events"
          :Key="event.id"
          :title="event.title"
          :when="event.date"
          :description="event.description"
          @readMore="console.log('Registered!')"
        />
      </template>
      <template v-else>
        <LoadingEventCard v-for="i in 4" :key="i" />
      </template>
    </section>

    <h2 class="text-2xl font-medium">Your Bookings</h2>
    <section class="grid grid-cols-1 gap-8" v-if="!bookingsLoading">
      <BookingItem
        v-for="booking in bookings"
        :key="booking.id"
        :title="booking.title"
        :when="booking.date"
        @click="console.log('booking')"
      />
    </section>
    <section v-else>Loading...bookings</section>
  </main>
</template>

<script setup>
import BookingItem from '@/components/BookingItem.vue';
import EventCard from '@/components/EventCard.vue';
import LoadingEventCard from '@/components/LoadingEventCard.vue';
import { onMounted, ref } from 'vue';

const API_URL = import.meta.env.VITE_API_URL;
const events = ref([]);
const eventsLoading = ref(true);
const bookings = ref([]);
const bookingsLoading = ref(true);

const fetchEvents = async () => {
  try {
    const res = await fetch(`${API_URL}/events`);
    events.value = await res.json();
    console.log(events.value);
  } finally {
    eventsLoading.value = false;
  }
};

const fetchBookings = async () => {
  try {
    const res = await fetch(`${API_URL}/bookings`);
    bookings.value = await res.json();
    console.log(bookings.value);
  } finally {
    bookingsLoading.value = false;
  }
};

onMounted(() => {
  fetchEvents();
  fetchBookings();
});
</script>
