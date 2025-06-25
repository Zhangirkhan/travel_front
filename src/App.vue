<script setup>
import { ref } from 'vue'
import Header from './components/Header/Header.vue'
import Hero from './components/Hero/Hero.vue'
import AccommodationTypes from './components/AccommodationTypes.vue'
import DirectionsTabs from './components/DirectionsTabs/DirectionsTabs.vue'
import GeniusBanner from './components/GeniusBanner.vue'
import CottagesBanner from './components/CottagesBanner/CottagesBanner.vue'
import Footer from './components/Footer/Footer.vue'

// Города и выпадающее меню
const cities = [
  'Los Angeles, USA',
  'New York, USA',
  'Almaty, KZ',
  'Astana, KZ',
  'London, UK'
]
const selectedCity = ref(cities[0])
const showCityMenu = ref(false)

// Языки и выпадающее меню
const languages = [
  { code: 'ru', label: 'RU' },
  { code: 'kz', label: 'KZ' },
  { code: 'en', label: 'EN' }
]
const selectedLang = ref('ru')
const showLangMenu = ref(false)

function selectCity(city) {
  selectedCity.value = city
  showCityMenu.value = false
}
function selectLang(code) {
  selectedLang.value = code
  showLangMenu.value = false
}

function onClickOutsideCityMenu(e) {
  if (!e.target.closest('.header-location')) showCityMenu.value = false
}
function onClickOutsideLangMenu(e) {
  if (!e.target.closest('.header-globe')) showLangMenu.value = false
}
if (typeof window !== 'undefined') {
  window.addEventListener('click', (e) => {
    onClickOutsideCityMenu(e)
    onClickOutsideLangMenu(e)
  })
}
</script>

<template>
  <Header
    :selectedCity="selectedCity"
    @toggle-city-menu="showCityMenu = !showCityMenu"
    @toggle-lang-menu="showLangMenu = !showLangMenu"
  >
    <template #city-menu>
      <div v-if="showCityMenu" class="dropdown-menu city-menu">
        <div v-for="city in cities" :key="city" class="dropdown-item" :class="{active: city === selectedCity}" @click.stop="selectCity(city)">
          {{ city }}
        </div>
      </div>
    </template>
    <template #lang-menu>
      <div v-if="showLangMenu" class="dropdown-menu lang-menu">
        <div v-for="lang in languages" :key="lang.code" class="dropdown-item" :class="{active: lang.code === selectedLang}" @click.stop="selectLang(lang.code)">
          {{ lang.label }}
        </div>
      </div>
    </template>
  </Header>

  <div class="main-bg">
    <!-- Hero with search -->
    <Hero />

    <AccommodationTypes />

    <DirectionsTabs />

    <!-- Блок: Путешествуйте больше, тратьте меньше -->
    <GeniusBanner />

    <!-- Блок: Найдите коттеджи для следующей поездки -->
    <CottagesBanner />

    <!-- FOOTER -->
    <Footer />
  </div>
</template>

<style scoped>
/* CSS Reset и базовые стили */
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body, .main-bg, .container, .main-header, .header-inner, .logo, .main-nav, .nav-link, .header-actions, .header-location, .header-login-btn, .genius-section, .genius-title, .genius-card, .genius-btn, .cottages-section, .cottages-card, .cottages-btn, .directions-section, .directions-title, .directions-tab, .direction-card, .footer-content, .footer-logo, .footer-desc, .footer-links, .footer-links li, .footer-bottom, .footer-bottom-left, .footer-bottom-right, .footer-bottom-right a {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Arial, sans-serif !important;
}
body {
  background: #f6f8fa;
  color: #18181b;
  min-height: 100vh;
}

.main-bg {
  min-height: 100vh;
  background: #f6f8fa;
}

/* Контейнер */
.container {
  max-width: 1280px;
  margin: 0 auto;
  width: 100%;
  padding: 0 0px;
}

/* Header */
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
  font-weight: bold;
  font-size: 1.4rem;
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
.profile-icon {
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.icon-circle {
  width: 28px;
  height: 28px;
  background: #e3e8ef;
  border-radius: 50%;
  display: inline-block;
}

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
.search-bar {
  position: absolute;
  left: 50%;
  bottom: -32px;
  transform: translateX(-50%);
  background: #fff;
  box-shadow: 0 4px 24px rgba(0,0,0,0.10);
  border-radius: 16px;
  display: flex;
  align-items: center;
  gap: 16px;
  padding: 0px 0px 0px 12px;
  min-width: 720px;
  max-width: 1280px;
  width: 100%;
  justify-content: space-between;
  ;
}
.search-item {
  display: flex;
  align-items: center;
  gap: 8px;
  background: #f6f8fa;
  border-radius: 8px;
  padding: 8px 14px;
  font-size: 1rem;
  width: 100%;
}
.search-label {
  color: #222;
}
.search-close {
  color: #aaa;
  font-size: 1.2rem;
  cursor: pointer;
}
.search-icon {
  font-size: 1.1rem;
  color: #2563eb;
}
.search-btn {
  background: #2563eb;
  color: #fff;
  border: none;
  border-radius: 8px;
  padding: 10px 28px;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  transition: background 0.2s;
  height: 70px;
}
.search-btn:hover {
  background: #1746b3;
}

/* Accommodation section */
.accommodation-section {
  max-width: 1280px;
  margin: 72px auto 0 auto;
  padding: 0px;
}
.section-title {
  font-size: 1.6rem;
  font-weight: bold;
  margin-bottom: 32px;
  color: #18181b;
}
.accommodation-list {
  display: flex;
  gap: 32px;
  flex-wrap: wrap;
  justify-content: space-between;
}
.accommodation-card {
  background: #fff;
  border-radius: 16px;
  box-shadow: 0 2px 12px rgba(0,0,0,0.06);
  width: 240px;
  padding-bottom: 18px;
  display: flex;
  flex-direction: column;
  align-items: center;
  transition: box-shadow 0.2s, transform 0.2s;
}
.accommodation-card:hover {
  box-shadow: 0 6px 24px rgba(37,99,235,0.10);
  transform: translateY(-4px) scale(1.03);
}
.acc-img {
  width: 220px;
  height: 140px;
  border-radius: 12px;
  background-size: cover;
  background-position: center;
  margin: 16px 0 12px 0;
}
.img1 {
  background-image: url('https://cf.bstatic.com/xdata/images/hotel/max1024x768/123456.jpg?k=1');
}
.img2 {
  background-image: url('https://cf.bstatic.com/xdata/images/hotel/max1024x768/654321.jpg?k=2');
}
.img3 {
  background-image: url('https://cf.bstatic.com/xdata/images/hotel/max1024x768/789123.jpg?k=3');
}
.img4 {
  background-image: url('https://cf.bstatic.com/xdata/images/hotel/max1024x768/321987.jpg?k=4');
}
.acc-title {
  font-size: 1.1rem;
  font-weight: 500;
  margin-bottom: 4px;
  color: #18181b;
  text-align: center;
}
.acc-count {
  color: #6b7280;
  font-size: 0.98rem;
  text-align: center;
}

@media (max-width: 900px) {
  .header-inner, .accommodation-section {
    padding: 0 12px;
  }
  .search-bar {
    min-width: 320px;
    flex-direction: column;
    gap: 10px;
    left: 50%;
    transform: translateX(-50%);
    padding: 12px 10px;
    max-width: 98vw;
   
  }
  .accommodation-list {
    gap: 16px;
    justify-content: center;
    
  }
  .accommodation-card {
    width: 90vw;
    max-width: 320px;
  }
  .acc-img {
    width: 90vw;
    max-width: 300px;
    height: 120px;
  }
}

.directions-section {
  margin-top: 48px;
  margin-bottom: 32px;
}
.directions-title {
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 8px;
}
.directions-subtitle {
  color: #6b7280;
  margin-bottom: 20px;
}
.directions-tabs {
  display: flex;
  gap: 16px;
  margin-bottom: 24px;
  flex-wrap: wrap;
}
.directions-tab {
  background: #f6f8fa;
  border: 1px solid #e5e7eb;
  border-radius: 24px;
  padding: 8px 18px;
  font-size: 1rem;
  color: #222;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 8px;
  transition: background 0.2s, border 0.2s, color 0.2s;
}
.directions-tab.active, .directions-tab:hover {
  background: #2563eb;
  color: #fff;
  border-color: #2563eb;
}
.tab-icon {
  font-size: 1.2em;
}
.directions-cards {
  display: flex;
  gap: 20px;
  overflow-x: auto;
  padding-bottom: 8px;
}
.direction-card {
  min-width: 180px;
  max-width: 200px;
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.06);
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  transition: box-shadow 0.2s, transform 0.2s;
  cursor: pointer;
}
.direction-card:hover {
  box-shadow: 0 6px 24px rgba(37,99,235,0.10);
  transform: translateY(-4px) scale(1.03);
}
.direction-img {
  width: 100%;
  height: 110px;
  border-radius: 12px 12px 0 0;
  background-size: cover;
  background-position: center;
}
.direction-title {
  font-size: 1.05rem;
  font-weight: 500;
  margin: 10px 0 2px 12px;
}
.direction-distance {
  color: #6b7280;
  font-size: 0.95rem;
  margin-left: 12px;
  margin-bottom: 10px;
}

.genius-section {
  margin-top: 40px;
  margin-bottom: 24px;
}
.genius-title {
  font-size: 1.25rem;
  font-weight: bold;
  margin-bottom: 16px;
}
.genius-card {
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.06);
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 20px 28px;
  gap: 24px;
}
.genius-card-left {
  flex: 1;
}
.genius-card-title {
  font-weight: 600;
  margin-bottom: 4px;
}
.genius-card-desc {
  color: #6b7280;
  margin-bottom: 12px;
}
.genius-card-actions {
  display: flex;
  gap: 12px;
}
.genius-btn {
  border: none;
  border-radius: 8px;
  font-size: 1rem;
  padding: 8px 20px;
  cursor: pointer;
  font-weight: 500;
  transition: background 0.2s, color 0.2s;
}
.genius-btn-primary {
  background: #2563eb;
  color: #fff;
}
.genius-btn-primary:hover {
  background: #1746b3;
}
.genius-btn-link {
  background: none;
  color: #2563eb;
  text-decoration: underline;
  padding: 8px 0;
}
.genius-btn-link:hover {
  color: #1746b3;
}
.genius-card-right {
  display: flex;
  align-items: center;
  justify-content: center;
}
.genius-badge {
  background: #2563eb;
  color: #fff;
  font-weight: bold;
  font-size: 1.1rem;
  border-radius: 8px;
  padding: 12px 24px;
  box-shadow: 0 2px 8px rgba(37,99,235,0.10);
  position: relative;
}
.genius-badge::after {
  content: '';
  position: absolute;
  right: -10px;
  top: -10px;
  width: 18px;
  height: 18px;
  background: #fffbe6;
  border-radius: 50%;
  z-index: -1;
}

.cottages-section {
  margin-top: 24px;
  margin-bottom: 32px;
}
.cottages-card {
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.06);
  display: flex;
  align-items: stretch;
  overflow: hidden;
  min-height: 180px;
}
.cottages-card-left {
  flex: 1.2;
  display: flex;
  align-items: center;
  justify-content: center;
  min-width: 0;
}
.cottages-circle {
  background: #0071c2;
  border-radius: 50%;
  width: 260px;
  height: 260px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 24px 0;
}
.cottages-text {
  color: #fff;
  font-size: 1.25rem;
  font-weight: 500;
  text-align: left;
  line-height: 1.3;
}
.cottages-link {
  text-decoration: underline;
  color: #fff;
  cursor: pointer;
}
.cottages-btn {
  margin-top: 18px;
  background: #fff;
  color: #0071c2;
  border: none;
  border-radius: 8px;
  font-size: 1rem;
  padding: 10px 18px;
  font-weight: 500;
  cursor: pointer;
  transition: background 0.2s, color 0.2s;
}
.cottages-btn:hover {
  background: #e6f0fa;
}
.cottages-card-right {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  min-width: 0;
  background: #f6f8fa;
}
.cottages-illustration {
  width: 120px;
  height: 120px;
  background: url('https://img.icons8.com/ios-filled/100/000000/armchair.png') center center/contain no-repeat;
  opacity: 0.8;
}

@media (max-width: 900px) {
  .genius-card, .cottages-card {
    flex-direction: column;
    align-items: flex-start;
    padding: 16px 10px;
    gap: 12px;
  }
  .cottages-circle {
    width: 180px;
    height: 180px;
    margin: 12px 0;
  }
  .cottages-illustration {
    width: 80px;
    height: 80px;
  }
}

.main-footer {
  background: #18191b;
  color: #fff;
  padding-top: 40px;
  padding-bottom: 0;
  margin-top: 48px;
}
.footer-content {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 32px;
  padding-bottom: 32px;
}
.footer-col {
  flex: 1;
}
.footer-logo-block {
  max-width: 320px;
}
.footer-logo {
  font-size: 2rem;
  font-weight: bold;
  margin-bottom: 12px;
}
.footer-desc {
  color: #d1d5db;
  font-size: 0.98rem;
  line-height: 1.5;
}
.footer-links-block {
  flex: 2;
  display: flex;
  justify-content: center;
}
.footer-links {
  display: flex;
  gap: 48px;
}
.footer-links ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
.footer-links li {
  margin-bottom: 10px;
  color: #fff;
  font-size: 1rem;
  cursor: pointer;
  transition: color 0.2s;
}
.footer-links li:hover {
  color: #2563eb;
}
.footer-qr-block {
  display: flex;
  align-items: flex-start;
  justify-content: flex-end;
}
.footer-qr {
  background: #fff;
  border-radius: 8px;
  padding: 8px;
  width: 120px;
  height: 120px;
}
.footer-bottom {
  border-top: 1px solid #444;
  padding: 16px 0 12px 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 1rem;
  color: #fff;
}
.footer-bottom-left {
  letter-spacing: 1px;
}
.footer-bottom-right a {
  color: #fff;
  margin-left: 24px;
  text-decoration: none;
  font-size: 0.98rem;
  transition: color 0.2s;
}
.footer-bottom-right a:hover {
  color: #2563eb;
}

@media (max-width: 900px) {
  .footer-content {
    flex-direction: column;
    gap: 24px;
    align-items: flex-start;
  }
  .footer-links {
    gap: 24px;
  }
  .footer-qr {
    width: 80px;
    height: 80px;
  }
  .footer-bottom {
    flex-direction: column;
    gap: 8px;
    font-size: 0.95rem;
    align-items: flex-start;
  }
  .footer-bottom-right a {
    margin-left: 0;
    margin-right: 16px;
  }
}

.header-actions {
  display: flex;
  align-items: center;
  gap: 18px;
}
.header-location {
  position: relative;
  cursor: pointer;
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
.header-arrow {
  font-size: 0.8em;
  margin-left: 4px;
  color: #888;
}
.dropdown-menu {
  position: absolute;
  top: 120%;
  left: 0;
  min-width: 170px;
  background: #fff;
  border-radius: 10px;
  box-shadow: 0 4px 16px rgba(0,0,0,0.10);
  z-index: 100;
  padding: 6px 0;
  margin-top: 2px;
  font-size: 1rem;
  color: #222;
}
.city-menu {
  left: 0;
}
.lang-menu {
  left: 0;
  min-width: 80px;
}
.dropdown-item {
  padding: 8px 18px;
  cursor: pointer;
  transition: background 0.18s, color 0.18s;
  white-space: nowrap;
}
.dropdown-item:hover, .dropdown-item.active {
  background: #2563eb;
  color: #fff;
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
    margin-left: 0;
    gap: 10px;
  }
  .header-login-btn {
    padding: 8px 12px;
    font-size: 0.98rem;
  }
}
</style>
