<template>
  <SectionCard>
    <div class="flex justify-between">
      <div>{{ title }}</div>
      <div>{{ when }}</div>
      <ReadButton variant="danger"> Cancel </ReadButton>
    </div>
  </SectionCard>
</template>

<script setup>
import ReadButton from './ReadButton.vue';
import SectionCard from './SectionCard.vue';

defineProps({
  title: String,
  when: String
});

defineEmits(['click']);
</script>
