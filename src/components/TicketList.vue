<template>
  <div class="ticket-grid">
    <TicketCard
      v-for="t in tickets"
      :key="t.id"
      :ticket="t"
      @toggleFavourite="$emit('toggleFavourite', $event)"
    />
  </div>
</template>

<script setup>
import TicketCard from './TicketCard.vue'

defineProps({
  tickets: Array
})
// defineEmits not necessary here; parent will catch the forwarded event
</script>

<style scoped>
.ticket-grid {
  display: grid;
  gap: 24px;
  grid-template-columns: 1fr;
}

@media (min-width: 768px) {
  .ticket-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1100px) {
  .ticket-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}
</style>
