<template>
  <RoundedCard>
    <h3 class="p-4 font-medium text-xl border-b border-gray-200">{{ title }}</h3>
    <p class="p-4 border-b border-gray-200">{{ when }}</p>
    <p class="p-4">{{ description }}</p>
    <section class="flex justify-end p-4">
      <ReadButton @click="$emit('readMore')">ReadMore</ReadButton>
    </section>
  </RoundedCard>
</template>

<script setup>
import ReadButton from './ReadButton.vue';
import RoundedCard from './RoundedCard.vue';

defineProps({
  title: String,
  when: String,
  description: String
});

defineEmits(['readMore']);
</script>
