<template>
  <section class="directions-section-full">
    <div class="directions-section container">
      <h2 class="directions-title">Спланируйте поездку легко и быстро</h2>
      <div class="directions-subtitle">Выберите вид отдыха и посмотрите лучшие места в США</div>
      <div class="directions-tabs">
        <button
          v-for="tab in tabs"
          :key="tab.key"
          :class="['directions-tab', { active: activeTab === tab.key }]"
          @click="activeTab = tab.key"
        >
          <span class="tab-icon">{{ tab.icon }}</span>
          {{ tab.label }}
        </button>
      </div>
      <div class="directions-cards">
        <div
          v-for="item in directions[activeTab]"
          :key="item.title"
          class="direction-card"
        >
          <div class="direction-img" :style="{ backgroundImage: `url('${item.img || 'https://placehold.co/400x256?text=Direction'}` }"></div>
          <div class="direction-info">
            <div class="direction-title">{{ item.title }}</div>
            <div class="direction-distance">{{ item.distance }}</div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const tabs = [
  { key: 'city', label: 'Город', icon: '🏙️' },
  { key: 'beach', label: 'Пляж', icon: '🏖️' },
  { key: 'ski', label: 'Горные лыжи', icon: '⛷️' },
  { key: 'nature', label: 'Природа', icon: '🌲' },
  { key: 'relax', label: 'Расслабляющий отдых', icon: '🧘' },
  { key: 'romantic', label: 'Романтика', icon: '💖' },
  { key: 'food', label: 'Еда', icon: '🍽️' },
]

const directions = {
  city: [
    { title: 'Сан-Луис-Обиспо', distance: '260 км от города Лос-Анджелес', img: '' },
    { title: 'Санта-Фе', distance: '1 136 км от города Лос-Анджелес', img: '' },
    { title: 'Cozad', distance: '1776 км от города Лос-Анджелес', img: '' },
    { title: 'Спрингфилд', distance: '2 609 км от города Лос-Анджелес', img: '' },
    { title: 'Берег', distance: '3 069 км от города Лос-Анджелес', img: '' },
    { title: 'Уинчестер', distance: '3 593 км от города Лос-Анджелес', img: '' },
  ],
  beach: [
    { title: 'Майами-Бич', distance: '3 800 км от города Лос-Анджелес', img: '' },
    { title: 'Санта-Моника', distance: '24 км от города Лос-Анджелес', img: '' },
    { title: 'Лагуна-Бич', distance: '80 км от города Лос-Анджелес', img: '' },
  ],
  ski: [
    { title: 'Аспен', distance: '1 400 км от города Лос-Анджелес', img: '' },
    { title: 'Вейл', distance: '1 500 км от города Лос-Анджелес', img: '' },
  ],
  nature: [
    { title: 'Йосемити', distance: '500 км от города Лос-Анджелес', img: '' },
    { title: 'Секвойя', distance: '350 км от города Лос-Анджелес', img: '' },
  ],
  relax: [
    { title: 'Палм-Спрингс', distance: '170 км от города Лос-Анджелес', img: '' },
  ],
  romantic: [
    { title: 'Сонома', distance: '650 км от города Лос-Анджелес', img: '' },
  ],
  food: [
    { title: 'Сан-Франциско', distance: '600 км от города Лос-Анджелес', img: '' },
  ],
}

const activeTab = ref('city')
</script>

<style scoped>
.directions-section-full {
  width: 100vw;
  position: relative;
  left: 50%;
  right: 50%;
  margin-left: -50vw;
  margin-right: -50vw;
  background: #fff;
}
.container {
  max-width: 1280px;
  margin: 0 auto;
  width: 100%;
  padding: 0 0px;
}
/* .directions-section {
  margin: 48px 0;
} */
.directions-title {
  font-size: 1.5rem;
  font-weight: 700;
  text-align: left;
  margin-bottom: 12px;
  color: #18181b;
}
.directions-subtitle {
  text-align: left;
  color: #6b7280;
  font-size: 1.1rem;
  margin-bottom: 32px;
}
.directions-tabs {
  display: flex;
  justify-content: start;
  gap: 8px;
  margin-bottom: 32px;
  flex-wrap: wrap;
}
.directions-tab {
  background: #fff;
  border: 1px solid #e5e7eb;
  border-radius: 50px 50px;
  padding: 12px 20px;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s;
  display: flex;
  align-items: center;
  gap: 8px;
  color: #6b7280;
}
.directions-tab:hover {
  border-color: #2563eb;
  color: #2563eb;
}
.directions-tab.active {
  background: #F2F6FE;
  border-color: #2563eb;
  color: #2563eb;
}
.tab-icon {
  font-size: 1.2rem;
}
.directions-cards {
  display: flex;
  gap: 32px;
  flex-wrap: wrap;
  justify-content: flex-start;
  align-items: stretch;
}
.direction-card {
  /* background: #fff; */
  border-radius: 24px;
  /* box-shadow: 0 4px 24px rgba(0,0,0,0.08); */
  width: 295px;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 0;
  transition: box-shadow 0.2s, transform 0.2s;
  overflow: hidden;
  padding: 32px 0 24px 0;
}
.direction-card:hover {
  /* box-shadow: 0 8px 32px rgba(37,99,235,0.10); */
  transform: translateY(-4px) scale(1.03);
}
.direction-img {
  width: 100%;
  height: 256px;
  border-radius: 16px;
  background-size: cover;
  background-position: center;
  margin-bottom: 20px;
}
.direction-info {
  display: flex;
  flex-direction: column;
  align-items: start;
  width: 100%;
}
.direction-title {
  font-size: 1.13rem;
  font-weight: 700;
  color: #18181b;
  margin-bottom: 6px;
  text-align: left;
}
.direction-distance {
  color: #6b7280;
  font-size: 1.01rem;
  font-weight: 400;
  text-align: left;
}
@media (max-width: 1280px) {
  .direction-card {
    width: 45vw;
    max-width: 295px;
  }
  .directions-cards {
    gap: 20px;
  }
}
@media (max-width: 700px) {
  .direction-card {
    width: 95vw;
    max-width: 295px;
    padding: 20px 0 16px 0;
  }
  .directions-cards {
    gap: 10px;
  }
  .direction-img {
    height: 100%;
    width: 100%;
  }
  .directions-title {
    font-size: 1.3rem;
    margin-bottom: 20px;
  }
}
</style> 