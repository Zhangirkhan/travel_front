<template>
  <section class="genius-section container">
    <div class="genius-card">
      <div class="genius-card-left">
        <div class="genius-card-title">Войдите в аккаунт и сэкономьте</div>
        <div class="genius-card-desc">Сэкономьте от 10% на вариантах жилья, отмеченных синим значком Genius.</div>
        <div class="genius-card-actions">
          <button class="genius-btn genius-btn-primary">Войти</button>
          <button class="genius-btn genius-btn-link">Зарегистрироваться</button>
        </div>
      </div>
      <div class="genius-card-right">
        <div class="genius-badge" @mouseenter="isShaking = true" @mouseleave="isShaking = false">
          <span class="genius-badge-gift" :class="{ shake: isShaking }">
            <img src="@/assets/photos/gift.webp" alt="Gift icon" width="128" height="128">
          </span>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
const isShaking = ref(false)
</script>

<style scoped>
/* Контейнер */
.container {
  max-width: 1280px;
  margin: 0 auto;
  width: 100%;
  padding: 0 0px;
}

.genius-section {
  margin-top: 40px;
  margin-bottom: 24px;
 
}
.genius-card {
  background: #fff;
  border-radius: 16px;
  box-shadow: 0 4px 24px rgba(0,0,0,0.08);
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 28px 36px;
  gap: 32px;
  
  width: 100%;
}
.genius-card-left {
  flex: 1;
}
.genius-card-title {
  font-weight: 600;
  margin-bottom: 4px;
  font-size: 1.5rem;
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
  padding: 12px 24px;
  cursor: pointer;
  font-weight: 500;
  transition: background 0.2s, color 0.2s;
}
.genius-btn-primary {
  background: #2563eb;
  color: #fff;
  padding: 14px 28px;
  font-size: 1.05rem;
}
.genius-btn-primary:hover {
  background: #1746b3;
}
.genius-btn-link {
  background: none;
  color: #2563eb;
  text-decoration: none;
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
  background: transparent;
  color: #fff;
  font-weight: bold;
  font-size: 1.1rem;
  border-radius: 12px;
  padding: 12px 24px;
  box-shadow: none;
  position: relative;
  display: flex;
  align-items: center;
  gap: 10px;
  cursor: pointer;
  user-select: none;
}
.genius-badge-gift {
  display: flex;
  align-items: center;
  transition: transform 0.3s cubic-bezier(.36,.07,.19,.97);
}
.genius-badge-gift.shake {
  animation: shake-gift 1.2s ease-in-out infinite;
}
@keyframes shake-gift {
  0%, 100% { transform: translateX(0); }
  10%, 30%, 50%, 70%, 90% { transform: translateX(-2px); }
  20%, 40%, 60%, 80% { transform: translateX(2px); }
}
.genius-badge-text {
  margin-left: 2px;
}
@media (max-width: 700px) {
  .genius-card {
    flex-direction: column;
    align-items: flex-start;
    padding: 16px 10px;
    gap: 12px;
  }
  .genius-badge {
    padding: 10px 16px;
    font-size: 1rem;
  }
}
</style> 