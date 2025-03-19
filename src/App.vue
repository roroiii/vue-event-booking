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
          @register="handleRegistration(event)"
        />
      </template>
      <template v-else>
        <LoadingEventCard v-for="i in 4" :key="i" />
      </template>
    </section>

    <h2 class="text-2xl font-medium">Your Bookings</h2>
    <section class="grid grid-cols-1 gap-8">
      <template v-if="!bookingsLoading">
        <BookingItem
          v-for="booking in bookings"
          :key="booking.id"
          :title="booking.eventTitle"
          :status="booking.status"
          @cancelled="handleCancelBooking(booking.id)"
        />
      </template>
      <template v-else>
        <LoadingBookingItem v-for="i in 4" :key="i" />
      </template>
    </section>
  </main>
</template>

<script setup>
import BookingItem from '@/components/BookingItem.vue';
import EventCard from '@/components/EventCard.vue';
import LoadingBookingItem from '@/components/LoadingBookingItem.vue';
import LoadingEventCard from '@/components/LoadingEventCard.vue';
import { onMounted, ref } from 'vue';

const API_URL = import.meta.env.VITE_API_URL;
const events = ref([]);
const eventsLoading = ref(true);
const bookings = ref([]);
const bookingsLoading = ref(true);

const findBookingById = (id) => bookings.value.findIndex((b) => b.id === id);

const fetchEvents = async () => {
  try {
    const res = await fetch(`${API_URL}/events`);
    events.value = await res.json();
  } finally {
    eventsLoading.value = false;
  }
};

const fetchBookings = async () => {
  try {
    const res = await fetch(`${API_URL}/bookings`);
    bookings.value = await res.json();
  } finally {
    bookingsLoading.value = false;
  }
};

const handleRegistration = async (event) => {
  if (bookings.value.some((booking) => booking.eventId === event.id && booking.userId === 1)) {
    alert('You have already registered for this event');
    return;
  }

  const newBooking = {
    id: Date.now().toString(),
    userId: 1,
    eventId: event.id,
    eventTitle: event.title
  };

  bookings.value.push(newBooking);

  try {
    const res = await fetch(`${API_URL}/bookings`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        ...newBooking,
        status: 'pending'
      })
    });

    if (res.ok) {
      const index = findBookingById(newBooking.id);
      bookings.value[index] = await res.json();
    } else {
      throw new Error('Failed to confirm booking');
    }
  } catch (error) {
    console.error(`Failed to register for event: `, error);
    bookings.value = bookings.value.filter((b) => b.id !== newBooking.id);
  }
};

const handleCancelBooking = async (bookingId) => {
  const index = findBookingById(bookingId);
  const originalBooking = bookings.value[index];
  bookings.value.splice(index, 1);

  try {
    const res = await fetch(`${API_URL}/bookings/${bookingId}`, {
      method: 'DELETE'
    });

    if (!res.ok) {
      throw new Error('Failed to cancel booking');
    }
  } catch (error) {
    console.error(`Failed to cancel booking: `, error);
    bookings.value.splice(index, 0, originalBooking);
  }
};

onMounted(() => {
  fetchEvents();
  fetchBookings();
});
</script>
