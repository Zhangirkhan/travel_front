<template>
  <section class="cottages-section container">
    <div class="cottages-card">
      <div class="cottages-card-left">
        <div class="cottages-blue-circle">
          <div class="cottages-text-block">
            <div class="cottages-title">Найдите <span class="cottages-link">коттеджи</span><br>для следующей поездки</div>
            <button class="cottages-btn">Узнать больше о домах и апартаментах</button>
          </div>
        </div>
        <div class="cottages-yellow-dot"></div>
      </div>
      <div class="cottages-card-right">
        <img class="cottages-illustration-img" src="@/assets/photos/divan2.png" alt="Диван" />
      </div>
    </div>
  </section>
</template>

<script setup>
// CottagesBanner component
</script>

<style scoped>
/* Контейнер */
.container {
  max-width: 1280px;
  margin: 0 auto;
  width: 100%;
  padding: 0 0px;
}

.cottages-section {
  margin: 48px 0;
}
.cottages-card {
  background: #fff;
  border-radius: 12px;
  padding: 0;
  display: flex;
  align-items: stretch;
  justify-content: space-between;
  gap: 0;
  box-shadow: 0 2px 8px rgba(0,0,0,0.04);
  position: relative;
  overflow: hidden;
}
.cottages-card-left {
  position: relative;
  flex: 1 1 0;
  min-width: 0;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  min-height: 320px;
}
.cottages-blue-circle {
  background: #0066e6;
  width: 620px;
  height: 520px;
  border-radius: 50%;
  position: absolute;
  left: 10%;
  top: 50%;
  transform: translateY(-50%);
  z-index: 1;
  display: flex;
  align-items: center;
  justify-content: center;
}
.cottages-text-block {
  position: relative;
  z-index: 2;
  color: #fff;
  text-align: left;
  padding: 0 40px;
  width: 340px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}
.cottages-title {
  font-size: 1.6rem;
  font-weight: 700;
  margin-bottom: 24px;
  line-height: 1.2;
}
.cottages-link {
  color: #fff;
  font-weight: 700;
  text-decoration: underline;
}
.cottages-btn {
  background: #fff;
  color: #0066e6;
  border: none;
  border-radius: 6px;
  padding: 12px 0;
  width: 100%;
  font-size: 1rem;
  font-weight: 500;
  margin-top: 0;
  box-shadow: 0 2px 8px rgba(0,0,0,0.03);
  cursor: pointer;
  transition: background 0.2s, color 0.2s;
}
.cottages-btn:hover {
  background: #e6f0ff;
  color: #0050b3;
}
.cottages-yellow-dot {
  position: absolute;
  left: -32px;
  top: 50%;
  transform: translateY(-50%);
  width: 48px;
  height: 48px;
  background: #FFC700;
  border-radius: 50%;
  z-index: 3;
}
.cottages-card-right {
  flex: 1 1 0;
  /* min-width: 0; */
  /* display: flex; */
  /* align-items: center; */
  /* justify-content: center; */
  background: none;
  position: relative;
  min-height: 100%;
}
.cottages-illustration-img {
  width: 100%;
  max-width: 100%;
  height: auto;
  display: block;
}
@media (max-width: 900px) {
  .cottages-card {
    flex-direction: column;
    align-items: stretch;
    min-height: 0;
  }
  .cottages-card-left, .cottages-card-right {
    min-height: 0;
    justify-content: center;
  }
  .cottages-blue-circle {
    width: 680px;
    height: 580px;
    left: 50%;
    transform: translate(-50%, -50%);
  }
  .cottages-text-block {
    width: 100%;
    padding: 0 16px;
  }
  .cottages-illustration-img {
    width: 220px;
  }
  .cottages-yellow-dot {
    left: -18px;
    width: 28px;
    height: 28px;
  }
}
</style> 