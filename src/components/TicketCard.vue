<script setup>
import { ref } from 'vue'

const props = defineProps({
  ticket: Object
})

const isOpen = ref(false)
const emit = defineEmits(['toggleFavourite'])

function toggleFavourite() {
  emit('toggleFavourite', props.ticket.id)
}

function bookTicket() {
  const confirmed = confirm(`Do you want to book: ${props.ticket.name}?`)
  if (confirmed) alert(`Successfully booked: ${props.ticket.name} 🎉`)
  else alert('Booking cancelled ❌')
}

function buyNow() {
  alert(`Redirecting to checkout for: ${props.ticket.name} 💳`)
}
</script>

<template>
  <div class="ticket-card" :class="{ featured: ticket.featured }">
    <img :src="ticket.img" :alt="ticket.name" class="ticket-image" />

    <h2>{{ ticket.name }}</h2>
    <p class="price">${{ ticket.price }}</p>

    <!-- Short description -->
    <p class="description">{{ ticket.description }}</p>

    <!-- Dropdown benefits -->
    <button class="toggle-btn" @click="isOpen = !isOpen">
      {{ isOpen ? "Hide Benefits ▲" : "Show Benefits ▼" }}
    </button>

    <ul v-if="isOpen" class="benefits-list">
      <li v-for="(benefit, i) in ticket.benefits" :key="i">• {{ benefit }}</li>
    </ul>

    <!-- Favourite button -->
    <button :class="{'fav-btn': true, 'favourited': ticket.favourited}" @click="toggleFavourite">
      {{ ticket.favourited ? "💔 Remove Favourite" : "❤️ Favourite" }}
    </button>

    <!-- Book & Buy Now -->
    <button class="book-btn" @click="bookTicket">🎟️ Book Ticket</button>
    <button class="cta-btn" @click="buyNow">💳 Buy Now</button>
  </div>
</template>

<style scoped>
.ticket-card {
  background: rgba(255,255,255,0.12);
  backdrop-filter: blur(8px);
  border-radius: 12px;
  padding: 20px;
  color: white;
  transition: transform 0.2s, box-shadow 0.2s;
  border: 1px solid rgba(255,255,255,0.18);
}

.ticket-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 20px rgba(0,0,0,0.3);
}

.featured {
  border: 3px solid gold;
  box-shadow: 0 0 15px gold;
}

.ticket-image {
  width: 100%;
  height: 180px;
  object-fit: cover;
  border-radius: 12px;
  margin-bottom: 12px;
}

.description {
  font-size: 0.95rem;
  color: #f0f0f0;
  margin: 8px 0 12px;
}

.toggle-btn {
  background: none;
  border: none;
  color: #ffd700;
  font-weight: bold;
  cursor: pointer;
  margin-top: 10px;
}

.benefits-list {
  margin-top: 8px;
  padding-left: 20px;
  font-size: 0.9rem;
}

.fav-btn, .book-btn, .cta-btn {
  width: 100%;
  padding: 10px;
  margin-top: 12px;
  border-radius: 10px;
  border: none;
  cursor: pointer;
  font-weight: bold;
  transition: 0.3s;
}

.fav-btn {
  background: #ff4d4d;
  color: white;
}

.fav-btn.favourited {
  animation: pulse 0.5s;
}

@keyframes pulse {
  0% { transform: scale(1); }
  50% { transform: scale(1.2); }
  100% { transform: scale(1); }
}

.fav-btn:hover { background: #e63535; }
.book-btn { background: #4CAF50; color: white; }
.book-btn:hover { background: #3d8b41; }
.cta-btn { background: #ff8c00; color: white; }
.cta-btn:hover { background: #e67600; }
</style>
