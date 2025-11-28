<template>
  <div class="ticket-list">
    <TicketCard
      v-for="ticket in tickets"
      :key="ticket.id"
      :ticket="ticket"
      @toggleFavourite="$emit('toggleFavourite', $event)"
    />
  </div>
</template>

<script setup>
import TicketCard from './TicketCard.vue'

defineProps({
  tickets: Array
})
defineEmits(['toggleFavourite'])
</script>

<style scoped>
.ticket-list {
  display: grid;
  gap: 20px;
}

@media (min-width: 768px) {
  .ticket-list {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .ticket-list {
    grid-template-columns: repeat(3, 1fr);
  }
}
</style>
