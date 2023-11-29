<template>
    <div class="feedback-form-modal">
        <button class="close-button" @click="closeForm">&times;</button>
        <form @submit.prevent="submitForm" ref="form">
            <h2>Обратная связь</h2>

            <!-- Поле Имя -->
            <label for="name">Имя:<span class="required-star">*</span></label>
            <input type="text" id="name" v-model="feedback.name" @blur="validateField('name')" required ref="name">

            <!-- Поле Email -->
            <label for="email">Email:</label>
            <input type="email" id="email" v-model="feedback.email" @blur="validateField('email')" ref="email">

            <!-- Поле Телефон -->
            <label for="phone">Телефон:<span class="required-star">*</span></label>
            <input type="tel" id="phone" v-model="feedback.phone" @blur="validateField('phone')" required
                @input="applyPhoneMask" pattern="\+7 \(\d{3}\) \d{3}-\d{2}-\d{2}" placeholder="+7(___)___-__-__"
                ref="phone">
            <!-- Поле Дата посещения -->
            <label for="date">Дата посещения:<span class="required-star">*</span></label>
            <input type="date" id="date" v-model="feedback.date" @blur="validateField('date')" required :max="today"
                ref="date">

            <!-- Поле Время посещения -->
            <label for="time">Время посещения:</label>
            <input type="time" id="time" v-model="feedback.time" min="10:00" max="22:00" @blur="validateField('time')"
                ref="time">

            <!-- Поле Количество гостей -->
            <label for="people">Количество гостей:</label>
            <input type="number" id="people" v-model="feedback.people" @blur="validateField('people')" min="1" max="20"
                ref="people">

            <!-- Поле Повод посещения -->
            <label for="occasion">Повод посещения:</label>
            <select id="occasion" v-model="feedback.occasion" @blur="validateField('occasion')" ref="occasion">
                <option value="business">Деловая встреча</option>
                <option value="pleasure">Удовольствие</option>
                <option value="other">Другое</option>
            </select>

            <!-- Поле Оценка обслуживания -->
            <label for="service-rating">Оценка обслуживания:<span class="required-star">*</span></label>
            <select id="service-rating" v-model="feedback.serviceRating" @blur="validateField('serviceRating')" required
                ref="serviceRating">
                <option value="">Выберите оценку</option>
                <option value="excellent">Отлично</option>
                <option value="good">Хорошо</option>
                <option value="fair">Удовлетворительно</option>
                <option value="poor">Плохо</option>
            </select>

            <!-- Поле Комментарии -->
            <label for="comments">Комментарии:<span class="required-star">*</span></label>
            <textarea id="comments" v-model="feedback.comments" maxlength="1000" @blur="validateField('comments')" required
                ref="comments"></textarea>

            <!-- Кнопка отправки -->
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
                phone: '',
                date: '',
                time: '',
                people: '',
                occasion: '',
                serviceRating: '',
                comments: ''
            },
            isSubmitted: false,
            today: new Date().toISOString().substring(0, 10),
        };
    },
    methods: {
        applyPhoneMask(event) {
            let value = event.target.value.replace(/\D/g, ''); // Убираем все нецифровые символы
            // Применяем маску только если длина числа достаточная
            if (value.length >= 1) {
                // Добавляем начальные +7, если их нет
                if (!value.startsWith('7')) {
                    value = '7' + value;
                }
                // Обрезаем до 11 символов
                value = value.substring(0, 11);

                // Форматируем номер
                let phoneNumber = '+7 ';
                if (value.length > 1) {
                    phoneNumber += '(' + value.substring(1, 4);
                }
                if (value.length >= 5) {
                    phoneNumber += ') ' + value.substring(4, 7);
                }
                if (value.length >= 8) {
                    phoneNumber += '-' + value.substring(7, 9);
                }
                if (value.length >= 10) {
                    phoneNumber += '-' + value.substring(9);
                }

                // Обновляем значение в модели Vue
                this.feedback.phone = phoneNumber;
            } else {
                this.feedback.phone = '';
            }
        },
        validateField(fieldName) {
            const field = this.$refs[fieldName];
            field.reportValidity()
        },
        submitForm() {
            this.isSubmitted = true;
            this.validateAllFields();
        },
        validateAllFields() {
            console.log('some')
        },
        closeForm() {
            this.isSubmitted = false;
            this.$emit('closeForm');
        },
        formatDate(date) {
            const year = date.getFullYear();
            const month = String(date.getMonth() + 1).padStart(2, "0");
            const day = String(date.getDate()).padStart(2, "0");
            return `${year}-${month}-${day}`;
        },
    }
};
</script>

<style scoped>
.feedback-form-modal {
    display: flex;
    flex-direction: column;
    position: absolute;
    top: 10vh;
    /* Форма будет начинаться на 10% от верха экрана, или установите конкретное значение в пикселях */
    left: 50%;
    transform: translateX(-50%);
    z-index: 1000;
    width: 90%;
    /* или ваша фиксированная ширина, если предпочитаете */
    max-width: 600px;
    /* Максимальная ширина */
    background: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    box-sizing: border-box;
    overflow-y: auto;
}

@media (max-width: 768px) {
    .feedback-form-modal {
        width: 100%;
        /* Форма занимает весь экран */
        top: 10vh;
        /* Или используйте фиксированное значение в пикселях, если необходимо */
        left: 0;
        transform: none;
    }
}

.feedback-form-modal h2 {
    font-family: 'Montserrat', sans-serif;
    /* Шрифт для заголовков */
    text-align: center;
    margin-bottom: 2rem;
    font-weight: 700;
    /* Делаем шрифт жирным */
    color: #333;
    /* Цвет текста, вы можете выбрать другой */
}

.feedback-form-modal form {
    display: flex;
    flex-direction: column;
    align-items: stretch;
}

.feedback-form-modal label {
    font-family: 'Roboto', sans-serif;
    /* Шрифт для описаний */
    margin-bottom: 0.5rem;
    font-weight: 400;
    /* Нормальное начертание текста */
    color: #444;
    /* Немного темнее для лучшей читаемости */
}

.feedback-form-modal input,
.feedback-form-modal select,
.feedback-form-modal textarea {
    font-family: 'Roboto', sans-serif;
    padding: 10px;
    margin-bottom: 1rem;
    /* Отступ снизу для каждого поля */
    border: 1px solid #ccc;
    border-radius: 4px;
    width: 100%;
    /* Это гарантирует, что элементы будут одинаковой ширины */
    box-sizing: border-box;
    /* Учитывает padding и border в общей ширине элемента */
}

.feedback-form-modal textarea {
    resize: vertical;
    height: 120px;
}

.feedback-form-modal button[type="submit"] {
    padding: 10px 15px;
    margin-top: 1rem;
    border: none;
    border-radius: 4px;
    background-color: #5cb85c;
    color: white;
    cursor: pointer;
    transition: background-color 0.3s ease;
    align-self: center;
}

.feedback-form-modal button[type="submit"]:hover,
.feedback-form-modal button[type="submit"]:focus {
    background-color: #4cae4c;
}

input:invalid {
    border: 2px solid red;
}

input:valid {
    border: 2px solid green;
}

.close-button {
    position: absolute;
    /* Позиционирование относительно ближайшего относительно позиционированного родителя */
    top: 1rem;
    /* Отступ сверху */
    right: 1rem;
    /* Отступ справа */
    background: none;
    /* Убрать фон */
    border: none;
    /* Убрать рамку */
    font-size: 1.5rem;
    /* Размер текста крестика */
    cursor: pointer;
    /* Курсор в виде указателя */
    color: #bbb;
    /* Цвет крестика */
}

.close-button:hover {
    color: #888;
    /* Цвет крестика при наведении */
}
</style>