<template>
  <div class="border border-gray-200 bg-white rounded-md">
    <h3 class="p-4 font-medium text-xl border-b border-gray-200">{{ title }}</h3>
    <p class="p-4 border-b border-gray-200">{{ when }}</p>
    <p class="p-4">{{ description }}</p>
    <section class="flex justify-end p-4">
      <!-- <button
        class="text-sm font-medium border border-gray-200 rounded-full px-3 py-1 hover:bg-gray-200"
        @click="$emit('readMore')"
      >
        ReadMore
      </button> -->
      <ReadButton @click="$emit('readMore')">ReadMore</ReadButton>
    </section>
  </div>
</template>

<script setup>
import ReadButton from './ReadButton.vue';

defineProps({
  title: String,
  when: String,
  description: String
});

defineEmits(['readMore']);
</script>
