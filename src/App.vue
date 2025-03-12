<template>
  <main class="container mx-auto my-8 space-y-8">
    <h1 class="text-4xl font-medium">Event Booking</h1>
    <h2 class="text-2xl font-medium">All Events</h2>
    <section class="grid grid-cols-2 gap-8">
      <EventCard
        v-for="i in 8"
        :Key="i"
        title="aaa"
        when="2025-03-11"
        description="bbb"
        @readMore="console.log('123')"
      />
    </section>
    <h2 class="text-2xl font-medium">Your Bookings</h2>
    <section class="grid grid-cols-1 gap-8">
      <BookingItem
        v-for="i in 3"
        :key="i"
        title="book"
        when="2025-03-12"
        description="book"
        @readMore="console.log('123')"
      />
    </section>
  </main>
</template>

<script setup>
import EventCard from '@/components/EventCard.vue';
import BookingItem from './components/BookingItem.vue';
</script>
