<script setup>
import { ref, computed } from 'vue'
import HeaderSection from './components/HeaderSection.vue'
import TicketList from './components/TicketList.vue'

const darkMode = ref(false)
const sortKey = ref('price')
const filterFeatured = ref('all')

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
      "VIP lounge",
      "Front-row seating",
      "Merch bundle",
      "Exclusive meet-and-greet"
    ]
  }
])

const filteredTickets = computed(() => {
  let list = [...tickets.value]
  if (filterFeatured.value === 'featured') {
    list = list.filter(t => t.featured)
  }
  return list.sort((a,b) => sortKey.value === 'price' ? a.price - b.price : a.name.localeCompare(b.name))
})

function toggleFavourite(id) {
  const t = tickets.value.find(x => x.id === id)
  t.favourited = !t.favourited
}
</script>

<template>
  <div :class="['page', { dark: darkMode }]">
    <HeaderSection
      title="Cape Town Food Festival 2025"
      subtitle="Choose your ticket tier and enjoy the experience!"
    />

    <!-- Controls -->
    <div class="controls">
      <label>
        Sort by:
        <select v-model="sortKey">
          <option value="price">Price</option>
          <option value="name">Name</option>
        </select>
      </label>

      <label>
        Filter:
        <select v-model="filterFeatured">
          <option value="all">All</option>
          <option value="featured">Featured Only</option>
        </select>
      </label>

      <button @click="darkMode = !darkMode">
        {{ darkMode ? '☀️ Light Mode' : '🌙 Dark Mode' }}
      </button>
    </div>

    <TicketList :tickets="filteredTickets" @toggleFavourite="toggleFavourite"/>
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

.page.dark {
  background: #1c1c1c;
  color: #e0e0e0;
}

.controls {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  align-items: center;
  margin: 20px 0;
}

.controls select, .controls button {
  padding: 8px 12px;
  border-radius: 8px;
  border: none;
  cursor: pointer;
}
</style>
