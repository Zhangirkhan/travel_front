<template>
  <section class="hero-section">
    <div class="hero-bg"></div>
    <div class="container container-search">
      <SearchBar />
    </div>
  </section>
</template>

<script setup>
import SearchBar from './SearchBar.vue'
</script>

<style scoped>
/* Hero section */
.hero-section {
  position: relative;
  height: 499px;
  width: 100vw;
  left: 50%;
  right: 50%;
  margin-left: -50vw;
  margin-right: -50vw;
  margin-bottom: 56px;
  background: #fff;
}
.hero-bg {
  width: 100vw;
  height: 100%;
  background: url('https://images.unsplash.com/photo-1506744038136-46273834b3fb?auto=format&fit=crop&w=1200&q=80') center center/cover no-repeat;
  border-bottom-left-radius: 12px;
  border-bottom-right-radius: 12px;
}
.container {
  max-width: 1280px;
  margin: 0 auto;
  width: 100%;
  position: relative;
  top: -60px;
  z-index: 2;
  display: flex;
  justify-content: center;
}

.container-search{
  max-width: 1140px;
}
</style> 