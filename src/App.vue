<template>
  <div class="container">
    <header>
      <h1 class="heading">Регистрация клиента</h1>
    </header>
    <section class="registry">
      <h2 class="registry__heading">Заполните поля формы</h2>
      <div class="registry__progress">
        <p class="registry__progress-text">{{ progress }} из 3</p>
        <div class="registry__progress-bar"></div>
      </div>
      <form novalidate>
        <fieldset v-if="progress === 1" class="form__container">
          <label
            class="form__label"
            :class="{ invalid: v$.patientData.personalInfo.lastName.$error }"
          >
            Фамилия
            <span class="form__requirement">*</span>
            <input
              type="text"
              class="form__input"
              @focus="v$.patientData.personalInfo.lastName.$touch"
              v-model="patientData.personalInfo.lastName"
              placeholder="Введите вашу фамилию"
            />
            <span class="form__error" v-if="v$.patientData.personalInfo.lastName.$error">
              Это обязательное поле
            </span>
          </label>
          <label
            class="form__label"
            :class="{ invalid: v$.patientData.personalInfo.firstName.$error }"
          >
            Имя
            <span class="form__requirement">*</span>
            <input
              type="text"
              class="form__input"
              @focus="v$.patientData.personalInfo.firstName.$touch"
              v-model="patientData.personalInfo.firstName"
              placeholder="Введите ваше имя"
            />
            <span class="form__error" v-if="v$.patientData.personalInfo.firstName.$error">
              Это обязательное поле
            </span>
          </label>
          <label class="form__label">
            Отчество
            <input
              type="text"
              class="form__input"
              v-model="patientData.personalInfo.surname"
              placeholder="Введите ваше отчество"
            />
          </label>
          <label
            class="form__label"
            :class="{ invalid: v$.patientData.personalInfo.birthDate.$error }"
          >
            Дата рождения
            <span class="form__requirement">*</span>
            <input
              type="date"
              class="form__input"
              @focus="v$.patientData.personalInfo.birthDate.$touch"
              v-model="patientData.personalInfo.birthDate"
            />
            <span class="form__error" v-if="v$.patientData.personalInfo.birthDate.$error">
              Это обязательное поле
            </span>
          </label>
          <label
            class="form__label"
            :class="{ invalid: v$.patientData.personalInfo.cellNumber.$error }"
          >
            Номер телефона
            <span class="form__requirement">*</span>
            <input
              type="number"
              class="form__input"
              placeholder="Введите ваш номер"
              @focus="v$.patientData.personalInfo.cellNumber.$touch"
              v-model="patientData.personalInfo.cellNumber"
            />
            <span class="form__error" v-if="v$.patientData.personalInfo.cellNumber.$error">
              {{ cellNumberValidationMessage }}
            </span>
          </label>
          <fieldset>
            <legend>Пол</legend>
            <label>
              <input
                name="gender"
                type="radio"
                value="мужской"
                v-model="patientData.personalInfo.gender"
              />
              Мужской
            </label>
            <label>
              <input
                name="gender"
                type="radio"
                value="женский"
                v-model="patientData.personalInfo.gender"
              />
              Женский
            </label>
          </fieldset>
          <fieldset class="form__group">
            <legend>
              Группа клиентов
              <span class="form__requirement">*</span>
            </legend>
            <label>
              <input name="patient-group" value="vip" type="checkbox" v-model="patientData.group" />
              VIP
            </label>
            <label>
              <input
                name="patient-group"
                value="problematic"
                type="checkbox"
                v-model="patientData.group"
              />
              Проблемные
            </label>
            <label>
              <input
                name="patient-group"
                value="insurance"
                type="checkbox"
                v-model="patientData.group"
              />
              ОМС
            </label>
            <span class="form__error" v-if="v$.patientData.group.$error">
              Это обязательное поле
            </span>
          </fieldset>
          <label>
            Лечащий врач
            <select name="therapist" class="form__select" v-model="patientData.therapist">
              <option value="">Выберите врача</option>
              <option value="ivanov">Иванов</option>
              <option value="zakharov">Захаров</option>
              <option value="chernysheva">Чернышева</option>
            </select>
          </label>
          <label>
            <input
              type="checkbox"
              name="no-messages"
              value="no-messages"
              v-model="patientData.noMessages"
            />
            Не отправлять СМС
          </label>
        </fieldset>
        <fieldset v-else-if="progress === 2" class="form__container">
          <label class="form__label">
            Индекс
            <input
              type="text"
              class="form__input"
              v-model="patientData.address.index"
              placeholder="Введите индекс"
            />
          </label>
          <label class="form__label">
            Страна
            <input
              type="text"
              class="form__input"
              v-model="patientData.address.country"
              placeholder="Введите индекс"
            />
          </label>
          <label class="form__label">
            Область
            <input
              type="text"
              class="form__input"
              v-model="patientData.address.region"
              placeholder="Введите индекс"
            />
          </label>
          <label class="form__label" :class="{ invalid: v$.patientData.address.city.$error }">
            Город
            <span class="form__requirement">*</span>
            <input
              type="text"
              class="form__input"
              @focus="v$.patientData.address.city.$touch"
              v-model="patientData.address.city"
              placeholder="Введите индекс"
            />
            <span class="form__error" v-if="v$.patientData.address.city.$error">
              Это обязательное поле
            </span>
          </label>
          <label class="form__label">
            Улица
            <input
              type="text"
              class="form__input"
              v-model="patientData.address.street"
              placeholder="Введите индекс"
            />
          </label>
          <label class="form__label">
            Дом
            <input
              type="text"
              class="form__input"
              v-model="patientData.address.houseNumber"
              placeholder="Введите индекс"
            />
          </label>
        </fieldset>
        <fieldset v-else class="form__container">
          <label>
            Тип документа
            <select name="document" class="form__select" v-model="patientData.passport.type">
              <option value="passport">Паспорт</option>
              <option value="birth-cert">Свидетельство о рождении</option>
              <option value="drivel-license">Вод. удостоверение</option>
            </select>
          </label>
          <label class="form__label">
            Серия
            <input
              type="text"
              class="form__input"
              v-model="patientData.passport.series"
              placeholder="Введите серию"
            />
          </label>
          <label class="form__label">
            Номер
            <input
              type="text"
              class="form__input"
              v-model="patientData.passport.number"
              placeholder="Введите номер"
            />
          </label>
          <label class="form__label">
            Кем выдан
            <input
              type="text"
              class="form__input"
              v-model="patientData.passport.issuedBy"
              placeholder="Введите кем выдан"
            />
          </label>
          <label
            class="form__label"
            :class="{ invalid: v$.patientData.passport.issuedWhen.$error }"
          >
            Дата выдачи
            <span class="form__requirement">*</span>
            <input
              type="date"
              class="form__input"
              @focus="v$.patientData.passport.issuedWhen.$touch"
              v-model="patientData.passport.issuedWhen"
            />
            <span class="form__error" v-if="v$.patientData.passport.issuedWhen.$error">
              Это обязательное поле
            </span>
          </label>
        </fieldset>
      </form>
      <div class="form__button-container">
        <button v-if="progress > 1" @click="decrementProgress" class="form__button" type="button">
          Назад
        </button>
        <button v-if="progress < 3" class="form__button" @click="incrementProgress" type="button">
          Далее
        </button>
        <button v-else :disabled="v$.$invalid" @click="submitHandler" class="form__button">
          Создать
        </button>
      </div>
    </section>
    <div
      class="success"
      :class="{ success_opened: successMessageVisible }"
      @click="clickOutsideSuccessPopup"
    >
      <div class="success__container">
        <div class="success__image"></div>
        <p class="success__text">Регистрация прошла успешно!</p>
        <button class="success__close-btn" type="button" @click="setSuccessMessageVisible"></button>
      </div>
    </div>
  </div>
</template>

<script>
import { maxLength, minLength, required } from '@vuelidate/validators';
import { useVuelidate } from '@vuelidate/core';
export default {
  name: 'app',
  data() {
    return {
      progress: 1,
      patientData: {
        personalInfo: {
          firstName: '',
          lastName: '',
          surname: '',
          birthDate: '',
          cellNumber: 7,
          gender: ''
        },
        address: {
          index: '',
          country: '',
          region: '',
          city: '',
          street: '',
          houseNumber: ''
        },
        passport: {
          type: 'passport',
          series: '',
          number: '',
          issuedBy: '',
          issuedWhen: ''
        },
        group: [],
        therapist: '',
        noMessages: false
      },
      successMessageVisible: false
    };
  },
  setup() {
    return {
      v$: useVuelidate()
    };
  },
  validations() {
    return {
      patientData: {
        personalInfo: {
          lastName: { required },
          firstName: { required },
          birthDate: { required },
          cellNumber: { required, minLength: minLength(11), maxLength: maxLength(20) }
        },
        address: {
          city: { required }
        },
        passport: {
          issuedWhen: { required }
        },
        group: { required }
      }
    };
  },
  methods: {
    incrementProgress() {
      this.progress++;
    },
    decrementProgress() {
      this.progress--;
    },
    setSuccessMessageVisible() {
      this.successMessageVisible = !this.successMessageVisible;
    },
    submitHandler() {
      if (this.v$.$invalid) {
        this.v$.$touch();
        return;
      }
      // отдаём на сервер
      console.log(JSON.parse(JSON.stringify(this.patientData)));

      // в then запроса
      this.resetFormFields();
      this.setSuccessMessageVisible();
      // редирект на другой путь
      // в catch – показываем ошибку
    },
    resetFormFields() {
      this.v$.$reset();
      this.patientData = {
        personalInfo: {
          firstName: '',
          lastName: '',
          surname: '',
          birthDate: '',
          cellNumber: 7,
          gender: ''
        },
        address: {
          index: '',
          country: '',
          region: '',
          city: '',
          street: '',
          houseNumber: ''
        },
        passport: {
          type: 'passport',
          series: '',
          number: '',
          issuedBy: '',
          issuedWhen: ''
        },
        group: [],
        therapist: '',
        noMessages: false
      };
    },
    clickOutsideSuccessPopup(e) {
      if (!this.$el.querySelector('.success__container').contains(e.target)) {
        this.setSuccessMessageVisible();
      }
    }
  },
  computed: {
    cellNumberValidationMessage() {
      if (this.v$.patientData.personalInfo.cellNumber.required.$invalid) {
        return 'Это обязательное поле';
      } else if (this.v$.patientData.personalInfo.cellNumber.minLength.$invalid) {
        return `Минимальная длина поля – ${this.v$.patientData.personalInfo.cellNumber.minLength.$params.min}`;
      } else {
        return `Максимальная длина поля – ${this.v$.patientData.personalInfo.cellNumber.maxLength.$params.max}`;
      }
    }
  }
};
</script>

<style lang="scss">
@import './assets/scss/_variables.scss';

.invalid {
  color: $input-invalid;
  .form__input {
    border: $input-invalid 1px solid;
  }
}

.container {
  padding-top: 80px;
}

header {
  margin-inline: auto;
  max-width: clamp(320px, 15vw, 500px);
  .heading {
    text-align: center;
    font-size: clamp(28px, 5vw, 30px);
  }
}

.registry {
  display: flex;
  flex-direction: column;
  margin: 30px auto 50px;
  max-width: clamp(330px, 60vw, 700px);
  background-color: #fff;
  border-radius: 20px;
  padding: 30px;
  box-shadow: 18px 18px 46px #729bc4;
}

.registry__heading {
  text-align: center;
  margin-bottom: 13px;

  @media screen and (max-width: 560px) {
    font-size: 20px;
  }
}

.registry__progress {
  height: 30px;
  margin-bottom: 25px;
}

.registry__progress-text {
  font-size: 14px;
  text-align: right;
  margin-bottom: 5px;
}

.registry__progress-bar {
  background-color: $progress-bar;
  height: 5px;
  position: relative;
  border-radius: 5px;

  &::before {
    content: '';
    background-color: $button-blue;
    border-radius: 5px;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 100;
    width: calc((v-bind(progress) / 3) * 100%);
    height: 100%;
    transition: width 0.3s ease;
  }
}

.form__container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 23px 44px;
  border: none;
  padding: 0;

  fieldset {
    border: none;
    padding: 0;

    label {
      display: block;
    }
  }

  @media screen and (max-width: 768px) {
    grid-template-columns: 1fr;
    gap: 23px;
  }
}

.form__label {
  position: relative;
  transition: color 0.3s ease-in-out;
  &:focus-within {
    color: $input-focused;

    .form__input {
      transition: border 0.4s ease-in-out;
      outline: none;
      border: $input-focused 1px solid;
    }
  }
}

.form__requirement {
  color: red;
}

.form__error {
  font-size: 13px;
  color: $input-invalid;
  position: absolute;
  top: 66px;
  left: 0;
  line-height: 1.15;
}

.form__input {
  max-width: 300px;
  width: 100%;
  display: block;
  border: $border-grey 1px solid;
  border-radius: 10px;
  padding: 10px;
  appearance: none;
  @media screen and (max-width: 768px) {
    width: 100%;
  }
}

.form__group {
  position: relative;
  .form__error {
    top: 75px;
  }
}

.form__select {
  display: block;
  margin-top: 5px;
  border: 1px solid #ccc;
  height: 30px;
}

.form__button-container {
  display: flex;
}

.form__button {
  appearance: none;
  border: none;

  background-color: $button-blue;
  color: #fff;
  font-size: large;
  border-radius: 8px;
  width: clamp(90px, 20vw, 200px);
  margin-top: 30px;
  padding-inline: 0;
  padding-block: 17px;
  margin-inline: auto;
  cursor: pointer;
  opacity: 1;
  transition: opacity 0.2s ease-out;

  &:hover {
    opacity: 0.7;
  }

  &:disabled {
    opacity: 0.4;
    cursor: auto;
  }

  @media screen and (max-width: 768px) {
  }
}

.success {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: hsla(0, 1%, 20%, 0);
  visibility: hidden;
  z-index: 101;
  transition: background 0.4s ease-in-out;

  &.success_opened {
    background-color: hsla(0, 1%, 20%, 0.3);
    visibility: visible;
  }

  .success__container {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: clamp(280px, 25vw, 300px);
    z-index: 102;
    background-color: #fff;
    border-radius: 20px;
    padding: 25px 5px;

    .success__image {
      background-image: url('./assets/images/success.png');
      background-size: contain;
      background-repeat: no-repeat;
      width: 100px;
      height: 100px;
      margin-inline: auto;
      margin-bottom: 20px;
    }

    .success__text {
      font-size: clamp(16px, 4vw, 20px);
      font-weight: 500;
      text-align: center;
    }

    .success__close-btn {
      background-image: url('./assets/images/close-btn.svg');
      background-size: contain;
      width: 40px;
      height: 40px;
      position: absolute;
      top: -40px;
      right: -40px;
      background-color: transparent;
      cursor: pointer;
      opacity: 1;
      transition: opacity 0.3s ease-in;

      &:hover {
        opacity: 0.7;
      }

      @media screen and (max-width: 368px) {
        right: 0;
        top: -45px;
      }
    }
  }
}
</style>
