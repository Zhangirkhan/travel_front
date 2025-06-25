<template>
  <section class="accommodation-types-section">
    <h2 class="accommodation-title">Поиск по типу размещения в городе Лос-Анджелес</h2>
    <div class="accommodation-list">
      <router-link 
        v-for="item in items" 
        :key="item.title" 
        :to="item.link" 
        class="accommodation-card-link"
      >
        <div class="accommodation-card">
          <div class="acc-img" :style="{ backgroundImage: `url('${item.img}')` }"></div>
          <div class="acc-info">
            <div class="acc-title">{{ item.title }}</div>
            <div class="acc-count">{{ item.count }}</div>
          </div>
        </div>
      </router-link>
    </div>
  </section>
</template>

<script setup>
import oteliImg from '@/assets/photos/hotels.png'
import apartImg from '@/assets/photos/apartments.png'
import resortImg from '@/assets/photos/resort-hotels.png'
import villaImg from '@/assets/photos/villas.png'

const items = [
  {
    title: 'Отели',
    count: '301 вариант',
    img: oteliImg,
    link: '/hotels'
  },
  {
    title: 'Апартаменты/квартиры',
    count: '410 вариант',
    img: apartImg,
    link: '/apartments'
  },
  {
    title: 'Курортные отели',
    count: '155 вариант',
    img: resortImg,
    link: '/resort-hotels'
  },
  {
    title: 'Виллы',
    count: '25 вариант',
    img: villaImg,
    link: '/villas'
  },
]
</script>

<style scoped>
.accommodation-types-section {
  background: #fff;
  padding: 48px 0 48px 0;
}
.accommodation-types-section .accommodation-title,
.accommodation-types-section .accommodation-list {
  max-width: 1280px;
  margin-left: auto;
  margin-right: auto;
  padding-left: 0px;
  padding-right: 0px;
}
.accommodation-title {
  font-size: 1.5rem;
  font-weight: 700;
  text-align: left;
  margin-bottom: 10px;
  color: #18181b;
}
.accommodation-list {
  display: flex;
  gap: 32px;
  justify-content: space-between;
  align-items: flex-start;
  flex-wrap: wrap;
  max-width: 1400px;
  margin: 0 auto;
}
.accommodation-card-link {
  text-decoration: none;
  color: inherit;
  display: block;
}
.accommodation-card {
  background: #fff;
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
.accommodation-card:hover {
  /* box-shadow: 0 8px 32px rgba(37,99,235,0.10); */
  transform: translateY(-4px) scale(1.03);
}
.acc-img {
  width: 100%;
  height: 256px;
  border-radius: 16px;
  background-size: cover;
  background-position: center;
  margin-bottom: 20px;
  box-shadow: 0 2px 8px rgba(37,99,235,0.10);
  border: 4px solid #f6f8fa;
}
.acc-info {
  display: flex;
  flex-direction: column;
  align-items: start;
  width: 100%;
}
.acc-title {
  font-size: 1.13rem;
  font-weight: 700;
  color: #18181b;
  margin-bottom: 6px;
  text-align: center;
}
.acc-count {
  color: #6b7280;
  font-size: 1.01rem;
  font-weight: 400;
  text-align: center;
}
@media (max-width: 1280px) {
  .accommodation-card {
    width: 45vw;
    max-width: 220px;
  }
  .accommodation-list {
    gap: 20px;
  }
}
@media (max-width: 700px) {
  .accommodation-card {
    width: 95vw;
    max-width: 220px;
    padding: 20px 0 16px 0;
  }
  .accommodation-list {
    gap: 10px;
  }
  .acc-img {
    height: 100%;
    width: 100%;
  }
  .accommodation-title {
    font-size: 1.3rem;
    margin-bottom: 20px;
  }
}
</style> 