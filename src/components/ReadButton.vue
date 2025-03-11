<template>
  <button
    class="text-sm font-medium border border-gray-200 rounded-full px-3 py-1 hover:bg-gray-200"
    @click="$emit('click')"
  >
    {{ label }}
  </button>
</template>

<script setup>
defineProps({
  label: String
});

defineEmits(['click']);
</script>
