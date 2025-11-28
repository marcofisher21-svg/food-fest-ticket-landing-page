<script setup>
import { ref, computed } from 'vue'
import HeaderSection from './components/HeaderSection.vue'
import TicketList from './components/TicketList.vue'

// Light/Dark Mode Toggle
const darkMode = ref(false)

// Sorting & Filtering
const sortMode = ref('none')
const filterMode = ref('all')

// Ticket Data
const tickets = ref([
  {
    id: 1,
    name: "Standard Pass",
    description: "Access to general sessions.",
    price: 50,
    featured: false,
    favourited: false,
    img: "https://i.postimg.cc/8zjcXtzM/images-q-tbn-ANd9Gc-Qr-RF4G2ow-M7OG-PZl-V2j-YVWFI9POjs6tsx8A-s.jpg",
    benefits: [
      "General seating",
      "Festival floor access",
      "Standard support"
    ]
  },
  {
    id: 2,
    name: "Premium Pass",
    description: "Priority seating + Q&A.",
    price: 89,
    featured: false,
    favourited: false,
    img: "https://i.postimg.cc/0NSQPjST/images-q-tbn-ANd9Gc-Sk-Te-J3YI9IK-q-u8q-Rw-KOCXj-YJ9olkby-Bc-Kw-s.jpg",
    benefits: [
      "Priority seating",
      "Guest speaker Q&A",
      "Snack voucher"
    ]
  },
  {
    id: 3,
    name: "VIP Experience",
    description: "VIP lounge + merch + front-row seating.",
    price: 119,
    featured: true,
    favourited: false,
    img: "https://i.postimg.cc/ZRF5vQVV/images-q-tbn-ANd9Gc-S-i-KJGrl-Qm-AWn-P9Y7VZIe-Sn-TYMVa5MOb-EA-s.jpg",
    benefits: [
      "Access to VIP lounge",
      "Exclusive merchandise",
      "Front-row seating"
    ]
  }
])

// Favourite Toggle
function toggleFavourite(id) {
  const t = tickets.value.find(t => t.id === id)
  if (t) t.favourited = !t.favourited
}

// Filtering + Sorting Logic
const processedTickets = computed(() => {
  let list = [...tickets.value]

  // FILTER
  if (filterMode.value === 'featured') {
    list = list.filter(t => t.featured)
  }

  // SORT
  if (sortMode.value === 'low') {
    list.sort((a, b) => a.price - b.price)
  } else if (sortMode.value === 'high') {
    list.sort((a, b) => b.price - a.price)
  }

  return list
})
</script>

<template>
  <div class="page" :class="{ dark: darkMode }">
    <HeaderSection />

    <!-- Controls Section -->
    <div class="controls">
      <!-- Sort -->
      <select v-model="sortMode">
        <option value="none">Sort: None</option>
        <option value="low">Price: Low → High</option>
        <option value="high">Price: High → Low</option>
      </select>

      <!-- Filter -->
      <select v-model="filterMode">
        <option value="all">Show: All</option>
        <option value="featured">Show: Featured</option>
      </select>

      <!-- Dark/Light Mode Toggle -->
      <button @click="darkMode = !darkMode">
        {{ darkMode ? '☀ Light Mode' : '🌙 Dark Mode' }}
      </button>
    </div>

    <TicketList
      :tickets="processedTickets"
      @toggleFavourite="toggleFavourite"
    />
  </div>
</template>

<style>
.page {
  min-height: 100vh;
  padding: 20px;
  font-family: system-ui;
  background: radial-gradient(circle, rgba(42, 37, 133, 1) 0%, rgba(178, 199, 22, 1) 35%, rgba(117, 46, 143, 1) 100%);
  color: white;
  transition: background 0.5s, color 0.5s;
}

/* DARK MODE */
.page.dark {
  background: #121212;
  color: #e0e0e0;
}

.controls {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  align-items: center;
  justify-content: center;
  margin: 20px 0;
}

.controls select,
.controls button {
  padding: 8px 12px;
  border-radius: 8px;
  border: none;
  cursor: pointer;
  font-weight: bold;
}
</style>
