<template>
  <div id="app">
    <TushevNavbar />
    <div class="button-container">
      <button @click="showModal = true">Оставить отзыв</button>
    </div>
    <div class="form-container">
      <FeedbackForm v-if="showModal" @formSubmitted="showModal = false" @closeForm="closeForm" />
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
    closeForm() {
      this.showModal = false
    },
    submitForm() {
      console.log(this.name);  // здесь логика отправки формы
      // обработка данных формы
      this.showModal = false; // закрыть модальное окно после отправки формы
    }
  }
};
</script>

<style>

body {
  background-image: url('./assets/background.png');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  background-attachment: fixed; /* Опционально, если хотите чтобы фон не прокручивался */
}

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
