<template>
  <nav class="navbar">
    <div class="navbar-brand">ТУШЕВ</div>
    <div class="navbar-menu">
      <div class="navbar-item">Главная</div>
      <div class="navbar-item">Меню</div>
      <div class="navbar-item">О нас</div>
      <div class="navbar-item">Контакты</div>
    </div>
  </nav>
</template>
  
<script>
export default {
  name: 'TushevNavbar',
  // Тут могут быть props, data, methods и т.д., если они нужны для навбара
};
</script>
  
<style>
html, body {
  margin: 0;
  padding: 0;
}

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #201f1f; /* Тёмный фон для навбара */
  color: white;
  margin: 0;
  padding: 0.5rem 1rem; /* Отступы внутри навбара */
  box-sizing: border-box; /* Убедитесь, что padding не влияет на общую ширину */
}

.navbar-brand {
  color: darkgoldenrod;
  font-weight: bold;
  font-size: 2.0rem; /* Увеличиваем размер шрифта */
  margin-left: 2rem; /* Добавляем немного отступа слева */
  letter-spacing: 0.2rem; /* Расстояние между буквами для лучшего вида */
  font-family: 'Lobster'; /* Изменение шрифта, если нужно */
}

.navbar-menu {
  display: flex;
}

.navbar-item {
  padding: 0.5rem 1rem;
  cursor: pointer;
  font-size: 1rem; /* Устанавливаем размер шрифта для элементов меню */
  font-family: 'Segoe UI', sans-serif; /* Шрифт, согласующийся с брендом */
}

.navbar-item:not(:last-child) {
  margin-right: 1rem; /* Отступ между элементами навбара */
}

/* Стили для навбара при наведении мыши */
.navbar-item:hover {
  background-color: #555;
  border-radius: 5px;
  transition: background-color 0.3s; /* Плавный переход для фона элементов меню */
}
</style>
  