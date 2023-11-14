<template>
  <div class="container">
    <header>
      <h1 class="heading">Регистрация клиента</h1>
    </header>
    <section class="registry">
      <h2 class="registry__heading">Заполните поля формы</h2>
      <div>
        <p>{{ progress }}</p>
        <div></div>
      </div>
      <form novalidate>
        <fieldset class="form__container">
          <label class="form__label">
            Фамилия
            <span class="form__requirement">*</span>
            <input type="text" class="form__input" placeholder="Введите вашу фамилию" />
          </label>
          <label class="form__label">
            Имя
            <span class="form__requirement">*</span>
            <input type="text" class="form__input" placeholder="Введите ваше имя" />
          </label>
          <label class="form__label">
            Отчество
            <input type="text" class="form__input" placeholder="Введите ваше отчество" />
          </label>
          <label class="form__label">
            Дата рождения
            <span class="form__requirement">*</span>
            <input type="date" class="form__input" />
          </label>
          <label class="form__label">
            Номер телефона
            <span class="form__requirement">*</span>
            <input
              type="tel"
              class="form__input"
              placeholder="Введите ваш номер"
              value="7"
              size="11"
            />
          </label>
          <fieldset>
            <legend>Пол</legend>
            <label>
              <input name="gender" type="radio" value="man" />
              Мужской
            </label>
            <label>
              <input name="gender" type="radio" value="woman" />
              Женский
            </label>
          </fieldset>
          <fieldset>
            <legend>
              Группа клиентов
              <span class="form__requirement">*</span>
            </legend>
            <label>
              <input name="patient-group" value="vip" type="checkbox" />
              VIP
            </label>
            <label>
              <input name="patient-group" value="problematic" type="checkbox" />
              Проблемные
            </label>
            <label>
              <input name="patient-group" value="insurance" type="checkbox" />
              ОМС
            </label>
          </fieldset>
          <label>
            Лечащий врач
            <select name="therapist" class="form__doctor-select">
              <option value="">Выберите врача</option>
              <option value="ivanov">Иванов</option>
              <option value="zakharov">Захаров</option>
              <option value="chernysheva">Чернышева</option>
            </select>
          </label>
          <label>
            <input type="checkbox" name="no-messages" value="no-messages" />
            Не отправлять СМС
          </label>
        </fieldset>
      </form>
      <button class="form__button" type="button">Далее</button>
    </section>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      progress: ''
    };
  }
};
</script>

<style lang="scss">
@import './assets/scss/_variables.scss';
.container {
  padding-top: 150px;
}

.heading {
  text-align: center;
}

.registry {
  display: flex;
  flex-direction: column;
  margin-top: 30px;
  margin-inline: auto;
  max-width: clamp(350px, 40vw, 650px);
  border: $border-grey 1px solid;
  background-color: #fff;
  border-radius: 20px;
  padding: 30px;
}

.registry__heading {
  text-align: center;
  margin-bottom: 13px;
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
}

.form__label {
  &:focus-within {
    color: $input-focused;

    .form__input {
      outline: none;
      border: $input-focused 1px solid;
    }
  }

  &:invalid {
    color: $input-invalid;
    .form__input {
      border: $input-invalid 1px solid;
    }
  }
}

.form__requirement {
  color: red;
}

.form__input {
  max-width: 285px;
  width: 100%;
  display: block;
  border: $border-grey 1px solid;
  border-radius: 10px;
  padding: 10px;
  appearance: none;
}

.form__doctor-select {
  //appearance: none;
  display: block;
  margin-top: 5px;
  border: 1px solid #ccc;
  height: 30px;
}

.form__button {
  appearance: none;
  border: none;

  background-color: $button-blue;
  color: #fff;
  font-size: large;
  border-radius: 8px;
  width: clamp(180px, 3vw, 200px);
  margin-top: 20px;
  padding-inline: 0;
  padding-block: 17px;
  margin-inline: auto;
  cursor: pointer;
  opacity: 1;
  transition: opacity 0.3s ease-in;

  &:hover {
    opacity: 0.7;
  }
}
</style>
