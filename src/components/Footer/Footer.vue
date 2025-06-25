<template>
  <footer class="main-footer">
    <div class="footer-content container">
      <div class="footer-col footer-logo-block">
        <div class="footer-logo">LOGO</div>
        <div class="footer-desc">
          Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived
        </div>
      </div>
      <div class="footer-col footer-links-block">
        <div class="footer-links">
          <ul>
            <li>Туры</li>
            <li>Отели</li>
            <li>Рестораны</li>
            <li>Аренда авто</li>
            <li>Развлечения</li>
          </ul>
          <ul>
            <li>Вакансии</li>
            <li>Связаться с нами</li>
            <li>Контакты</li>
            <li>Партнерам</li>
            <li>Оставить отзыв</li>
          </ul>
        </div>
      </div>
      <div class="footer-col footer-qr-block">
        <img class="footer-qr" src="https://api.qrserver.com/v1/create-qr-code/?size=120x120&data=https://example.com" alt="QR code" />
      </div>
    </div>
    <div class="footer-bottom container">
      <div class="footer-bottom-left">TOO GOODY KAZAKHSTAN</div>
      <div class="footer-bottom-right">
        <a href="#">Политика конфиденциальности</a>
        <a href="#">Пользовательское соглашение</a>
      </div>
    </div>
  </footer>
</template>

<script setup>
// Footer component
</script>

<style scoped>
/* Контейнер */
.container {
  max-width: 1280px;
  margin: 0 auto;
  width: 100%;
  padding: 0 0px;
}

.main-footer {
  background: #18191b;
  color: #fff;
  padding-top: 40px;
  padding-bottom: 0;
  margin-top: 48px;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Arial, sans-serif;
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
</style> 