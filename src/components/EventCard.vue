<template>
  <SectionCard>
    <template #header>
      {{ title }}
    </template>

    <template #when>
      {{ when }}
    </template>

    {{ description }}

    <template #footer>
      <ReadButton @click="$emit('readMore')">ReadMore</ReadButton>
    </template>
  </SectionCard>
</template>

<script setup>
import ReadButton from './ReadButton.vue';
import SectionCard from './SectionCard.vue';

defineProps({
  title: String,
  when: String,
  description: String
});

defineEmits(['readMore']);
</script>
