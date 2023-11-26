<template>
  <div id="app">
    <TushevNavbar />
    <div class="button-container">
      <button @click="showModal = true">Оставить отзыв</button>
    </div>
    <div class="form-container">
      <FeedbackForm v-if="showModal" @formSubmitted="showModal = false" />
    </div>
  </div>
</template>

<script>
import TushevNavbar from './components/TushevNavbar.vue';
import FeedbackForm from './components/FeedbackForm.vue';
export default {
  name: 'App',
  components: {
    TushevNavbar,
    FeedbackForm
  },

  data() {
    return {
      showModal: false,
    };
  },
  methods: {
    submitForm() {
      console.log(this.name);  // здесь логика отправки формы
      // обработка данных формы
      this.showModal = false; // закрыть модальное окно после отправки формы
    }
  }
};
</script>

<style>
#app {
  height: 100vh;
  /* Задает высоту всего приложения равной высоте видимой области браузера */
  background-image: url('./assets/background.png');
  /* Путь к вашему фоновому изображению */
  background-size: cover;
  /* Обеспечивает покрытие всего доступного пространства */
  background-position: center;
  /* Центрирует изображение */
  background-repeat: no-repeat;
  /* Предотвращает повторение изображения */
}

/* .form-container {
  position: absolute;

} */

.button-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: calc(100vh - 60px);
  /* Вычитаем высоту навбара, если она есть */
  margin-top: -60px;
  /* Поднимаем контейнер вверх на высоту навбара, если нужно */
}

button {
  padding: 1rem 2rem;
  font-size: 1.25rem;
  color: #fff;
  background-color: darkgoldenrod;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: rgb(166, 122, 10);
  /* Цвет кнопки при наведении */
}</style>
