<template>
  <SectionCard>
    <div class="p-4">booking</div>
  </SectionCard>
</template>

<script setup>
import SectionCard from './SectionCard.vue';

defineProps({
  title: String,
  when: String
});

defineEmits(['readMore']);
</script>
