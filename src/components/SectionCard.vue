<template>
  <RoundedCard>
    <h3 class="p-4 font-medium text-xl border-b border-gray-200">
      <slot name="header"></slot>
    </h3>
    <p class="p-4 border-b border-gray-200">
      <slot name="when"></slot>
    </p>
    <p class="p-4">
      <slot></slot>
    </p>
    <section class="flex justify-end p-4">
      <slot name="footer"></slot>
    </section>
  </RoundedCard>
</template>

<script setup>
import RoundedCard from './RoundedCard.vue';
</script>
