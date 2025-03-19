<template>
  <SectionCard>
    <div class="flex justify-between">
      <div class="flex space-x-2">
        <div>{{ title }}</div>
        <div>{{ status }}</div>
      </div>
      <ReadButton variant="danger" @click="$emit('cancelled')">Cancel</ReadButton>
    </div>
  </SectionCard>
</template>

<script setup>
import ReadButton from './ReadButton.vue';
import SectionCard from './SectionCard.vue';

defineProps({
  title: String,
  status: String
});

defineEmits(['cancelled']);
</script>
