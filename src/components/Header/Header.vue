<template>
  <header class="main-header">
    <div class="header-inner">
      <div class="header-left">
        <div class="logo">LOGO</div>
        <nav class="main-nav">
          <a href="#" class="nav-link">Туры</a>
          <a href="#" class="nav-link">Отели</a>
          <a href="#" class="nav-link">Рестораны</a>
          <a href="#" class="nav-link">Аренда авто</a>
          <a href="#" class="nav-link">Развлечения</a>
        </nav>
      </div>
      <div class="header-right">
        <div class="header-actions">
          <span class="header-location" @click.stop="$emit('toggle-city-menu')">
            📍
            <span class="header-location-text">{{ selectedCity }}</span>
            <span class="header-arrow">▼</span>
            <slot name="city-menu"></slot>
          </span>
          <span class="header-icon header-globe" @click.stop="$emit('toggle-lang-menu')">
            🌐
            <span class="header-arrow">▼</span>
            <slot name="lang-menu"></slot>
          </span>
          <button class="header-login-btn">Вход</button>
        </div>
      </div>
    </div>
  </header>
</template>

<script setup>
const props = defineProps({
  selectedCity: String
})
</script>

<style scoped>
.main-header {
  background: #fff;
  box-shadow: 0 2px 8px rgba(0,0,0,0.04);
  position: sticky;
  top: 0;
  z-index: 10;
}
.header-inner {
  max-width: 1280px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 64px;
  padding: 0px;
}
.header-left{
  display: flex;
  gap: 30px;
  flex-direction: row;
  align-items: center;
}
.logo {
  font-size: 1.4rem;
  font-weight: bold;
  letter-spacing: 1px;
}
.main-nav {
  display: flex;
  gap: 32px;
}
.nav-link {
  color: #222;
  text-decoration: none;
  font-size: 1rem;
  font-weight: 500;
  transition: color 0.2s;
}
.nav-link:hover {
  color: #2563eb;
}
.header-right {
  display: flex;
  align-items: center;
}
.header-actions {
  display: flex;
  align-items: center;
  gap: 18px;
}
.header-location {
  position: relative;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 1rem;
  color: #222;
}
.header-icon {
  font-size: 1.25rem;
  display: flex;
  align-items: center;
}
.header-globe {
  position: relative;
  cursor: pointer;
  transition: color 0.2s;
  display: flex;
  align-items: center;
}
.header-globe:hover {
  color: #2563eb;
}
.header-arrow {
  font-size: 0.8em;
  margin-left: 4px;
  color: #888;
}
.header-login-btn {
  background: #2563eb;
  color: #fff;
  border: none;
  border-radius: 8px;
  height: 46px;
  width: 92px;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  transition: background 0.2s;
}
.header-login-btn:hover {
  background: #1746b3;
}
@media (max-width: 900px) {
  .header-actions {
    gap: 10px;
  }
  .header-login-btn {
    padding: 8px 12px;
    font-size: 0.98rem;
  }
}
</style> 