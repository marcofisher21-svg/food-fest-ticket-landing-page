<template>
  <div class="ticket-card" :class="{ featured: ticket.featured }">

    <!-- Image -->
    <div class="img-wrapper">
      <img :src="ticket.img" :alt="ticket.name" />
    </div>

    <!-- Title -->
    <h3 class="name">{{ ticket.name }}</h3>

    <!-- Description -->
    <p class="description">{{ ticket.description }}</p>

    <!-- Benefits Dropdown -->
    <details class="benefits">
      <summary>Show Benefits</summary>
      <ul>
        <li v-for="(b, i) in ticket.benefits" :key="i">{{ b }}</li>
      </ul>
    </details>

    <!-- Prices -->
    <p class="price">
      <strong>USD:</strong> ${{ ticket.price }}
    </p>

    <p class="price-zar">
      <strong>ZAR:</strong> R{{ toRand(ticket.price) }}
    </p>

    <!-- Favourite Button -->
    <button
      @click="$emit('toggleFavourite', ticket.id)"
      :class="['fav-btn', ticket.favourited ? 'active' : '']"
    >
      {{ ticket.favourited ? '❤️ Favourited' : '♡ Favourite' }}
    </button>

    <!-- Book Button -->
    <button class="book-btn">
      📘 Book Now
    </button>

  </div>
</template>

<script setup>

// USD → ZAR conversion (fixed rate)
function toRand(usd) {
  return (usd * 18.5).toFixed(2)
}
</script>

<style scoped>
.ticket-card {
  background: white;
  border-radius: 16px;
  padding: 16px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  transition: 0.2s;
  overflow: hidden;
}

.ticket-card:hover {
  transform: translateY(-4px);
}

/* Featured styling */
.featured {
  border: 3px solid gold;
  background: #fffce5;
}

.img-wrapper {
  width: 100%;
  height: 180px;
  overflow: hidden;
  border-radius: 12px;
}

img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.name {
  font-size: 1.4rem;
  margin-top: 12px;
  font-weight: bold;
}

.description {
  margin: 8px 0;
  color: #555;
}

.benefits {
  margin-bottom: 10px;
}

.price {
  font-size: 1.1rem;
  margin-top: 8px;
}

.price-zar {
  font-size: 1.1rem;
  color: green;
  font-weight: bold;
}

.fav-btn {
  width: 100%;
  padding: 10px;
  margin-top: 12px;
  border-radius: 10px;
  border: none;
  background: #ddd;
  cursor: pointer;
  transition: 0.2s;
}

.fav-btn.active {
  background: red;
  color: white;
}

.book-btn {
  width: 100%;
  padding: 10px;
  border-radius: 10px;
  margin-top: 10px;
  border: none;
  background: #4caf50;
  color: white;
  cursor: pointer;
}
</style>
