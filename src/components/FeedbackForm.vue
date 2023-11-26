<template>
    <div class="feedback-form-modal">
        <form @submit.prevent="submitForm">
            <h2>Форма обратной связи</h2>

            <label for="name">Имя:</label>
            <input type="text" id="name" v-model="feedback.name" required>

            <label for="email">Email:</label>
            <input type="email" id="email" v-model="feedback.email" required>

            <label for="message">Сообщение:</label>
            <textarea id="message" v-model="feedback.message" required></textarea>

            <!-- Можно добавить другие поля по необходимости -->

            <button type="submit">Отправить</button>
        </form>
    </div>
</template>
  
  
<script>
export default {
    name: 'FeedbackForm',
    data() {
        return {
            feedback: {
                name: '',
                email: '',
                message: ''
            }
        };
    },
    methods: {
        submitForm() {
            // Предположим, что у нас есть функция для отправки данных формы
            // Например, отправка на API или вывод в консоль
            console.log(this.feedback);
            this.$emit('formSubmitted'); // Уведомляем родительский компонент об отправке формы
            this.resetForm(); // Очищаем форму после отправки
        },
        resetForm() {
            this.feedback = { name: '', email: '', message: '' };
        }
    }
};
</script>
  
<style scoped>
.feedback-form-modal {
    /* position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%); */
    background: white;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    width: 100%;
    max-width: 500px;
    /* Максимальная ширина формы */
    margin: 0 auto;
    /* Центрируем форму */
    align-content: center;
}

.feedback-form-modal h2 {
    text-align: center;
    margin-bottom: 20px;
}

.feedback-form-modal form {
    display: flex;
    flex-direction: column;
}

.feedback-form-modal label {
    margin-top: 10px;
}

.feedback-form-modal input,
.feedback-form-modal textarea {
    padding: 10px;
    margin-top: 5px;
    border: 1px solid #ddd;
    border-radius: 5px;
    font-size: 16px;
}

.feedback-form-modal button {
    padding: 10px 15px;
    margin-top: 20px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
}

.feedback-form-modal button:hover {
    background-color: #0056b3;
}
</style>