<template>
  <div class="direction-card">
    <div class="direction-img" :style="{ backgroundImage: `url('${img}')` }"></div>
    <div class="direction-info">
      <div class="direction-title">{{ title }}</div>
      <div class="direction-distance">{{ distance }}</div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  img: String,
  title: String,
  distance: String
})
</script>

<style scoped>
.direction-card {
  background: #fff;
  border-radius: 16px;
  box-shadow: 0 4px 24px rgba(0,0,0,0.08);
  width: 220px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  overflow: hidden;
  transition: box-shadow 0.2s, transform 0.2s;
}
.direction-card:hover {
  box-shadow: 0 8px 32px rgba(37,99,235,0.10);
  transform: translateY(-4px) scale(1.03);
}
.direction-img {
  width: 100%;
  height: 120px;
  object-fit: cover;
  background-size: cover;
  background-position: center;
  border-radius: 0;
}
.direction-info {
  background: #fff;
  width: 100%;
  padding: 16px 14px 14px 14px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}
.direction-title {
  font-size: 1.08rem;
  font-weight: 700;
  color: #18181b;
  margin-bottom: 4px;
}
.direction-distance {
  color: #444;
  font-size: 0.98rem;
  font-weight: 400;
  margin-bottom: 0;
}
</style> 