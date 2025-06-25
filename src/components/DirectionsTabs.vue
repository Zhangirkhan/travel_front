<script setup>
import DirectionCard from './DirectionsTabs/DirectionCard.vue'
// ...остальной setup-код...
</script>

<template>
  <section class="directions-section container">
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
      <DirectionCard
        v-for="item in directions[activeTab]"
        :key="item.title"
        :img="item.img"
        :title="item.title"
        :distance="item.distance"
      />
    </div>
  </section>
</template> 