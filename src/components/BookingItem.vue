<template>
  <RoundedCard>
    <div class="p-4">booking</div>
  </RoundedCard>
</template>

<script setup>
import RoundedCard from './RoundedCard.vue';

defineProps({
  title: String,
  when: String
});

defineEmits(['readMore']);
</script>
