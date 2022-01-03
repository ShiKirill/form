<template>
  <div class="main">
    <Modal v-model="showModal" />
    <form class="form" @submit.prevent="onSubmit">
      <div class="info-block">
        <h3 class="info-block__title">Личные данные</h3>
        <div class="info-block__item">
          <label for="surname" class="info-block__label">Фамилия*</label>
          <input
            type="text"
            name="surname"
            id="surname"
            class="info-block__field"
            :class="{ 'block-error': $v.surname.$error }"
            @input="$v.surname.$touch"
            v-model.trim="surname"
          />
          <div class="error" v-if="$v.surname.$error">
            Поле обязательно для заполнения
          </div>
        </div>
        <div class="info-block__item">
          <label for="name" class="info-block__label">Имя*</label>
          <input
            type="text"
            name="name"
            id="name"
            class="info-block__field"
            :class="{ 'block-error': $v.name.$error }"
            @input="$v.name.$touch"
            v-model.trim="name"
          />
          <div class="error" v-if="$v.name.$error">
            Поле обязательно для заполнения
          </div>
        </div>
        <div class="info-block__item">
          <label for="patronymic" class="info-block__label">Отчество</label>
          <input
            type="text"
            name="patronymic"
            id="patronymic"
            class="info-block__field"
            v-model.trim="patronymic"
          />
        </div>
        <div class="info-block__item info-block__item_date">
          <label for="date" class="info-block__label">Дата рождения*</label>
          <input
            type="date"
            id="date"
            class="info-block__field"
            :class="{ 'block-error': $v.birthdate.$error }"
            @input="$v.birthdate.$touch"
            v-model="birthdate"
          />
          <div class="error" v-if="$v.birthdate.$error">
            Поле обязательно для заполнения
          </div>
        </div>
        <div class="info-block__item">
          <label for="phone" class="info-block__label">Номер телефона*</label>
          <input
            type="tel"
            id="phone"
            class="info-block__field"
            @input="phoneMask"
            @change="phoneMask"
            @focus="phoneMask"
            @blur="phoneMask"
            :value="phone"
            :class="{ 'block-error': $v.phone.$error }"
          />
          <div class="error" v-if="$v.phone.$error">
            Поле обязательно для заполнения
          </div>
        </div>
        <div class="info-block__item">
          <p class="info-block__label">Пол</p>
          <div class="info-block__item__gender">
            <input
              type="radio"
              class="info-block__field"
              id="male"
              name="gender"
              value="male"
              @click="gender = 'male'"
            />
            <label for="male">Мужской</label>
            <input
              type="radio"
              class="info-block__field"
              id="female"
              name="gender"
              value="female"
              @click="gender = 'female'"
            />
            <label for="female">Женский</label>
          </div>
        </div>
        <div class="info-block__item info-block__item_multiple">
          <label for="clients" class="info-block__label"
            >Группа клиентов*</label
          >
          <select
            class="info-block__field info-block__field_select"
            @change="setClientGroupe"
          >
            <option hidden disabled selected value=""></option>
            <option value="VIP">VIP</option>
            <option value="Проблемные">Проблемные</option>
            <option value="ОМС">ОМС</option>
          </select>
          <input
            type="text"
            id="clients"
            class="info-block__field"
            :value="clientGroupe"
            :class="{ 'block-error': $v.clientGroupe.$error }"
            disabled
          />
          <svg
            class="info-block__chevron"
            xmlns="http://www.w3.org/2000/svg"
            width="10"
            height="16"
            viewBox="0 0 10 16"
          >
            <path
              fill-rule="evenodd"
              d="M5 11L0 6l1.5-1.5L5 8.25 8.5 4.5 10 6l-5 5z"
            />
          </svg>
          <div class="error" v-if="$v.clientGroupe.$error">
            Поле обязательно для заполнения
          </div>
        </div>
        <div class="info-block__item">
          <label for="doctor" class="info-block__label">Лечащий врач</label>
          <select
            id="doctor"
            class="info-block__field info-block__field_select"
            @change="setDoctor"
          >
            <option hidden disabled selected value="">
              Выберите из списка
            </option>
            <option value="Ivanov">Иванов</option>
            <option value="Zaharov">Захаров</option>
            <option value="Chernisheva">Чернышева</option>
          </select>
        </div>
        <div class="info-block__item info-block__item_checkbox">
          <input
            type="checkbox"
            id="message"
            class="info-block__field"
            @change="sendMsg = !sendMsg"
          />
          <label for="message" class="info-block__label"
            >Не отправлять СМС.</label
          >
        </div>
      </div>
      <div class="info-block">
        <h3 class="info-block__title">Адрес</h3>
        <div class="info-block__item">
          <label for="country" class="info-block__label">Страна</label>
          <input
            type="text"
            id="country"
            class="info-block__field"
            v-model.trim="country"
          />
        </div>
        <div class="info-block__item">
          <label for="region" class="info-block__label">Область</label>
          <input
            type="text"
            id="region"
            class="info-block__field"
            v-model.trim="region"
          />
        </div>
        <div class="info-block__item">
          <label for="city" class="info-block__label">Город*</label>
          <input
            type="text"
            id="city"
            class="info-block__field"
            @input="$v.city.$touch"
            :class="{ 'block-error': $v.city.$error }"
            v-model.trim="city"
          />
          <div class="error" v-if="$v.city.$error">
            Поле обязательно для заполнения
          </div>
        </div>
        <div class="info-block__item">
          <label for="street" class="info-block__label">Улица</label>
          <input
            type="text"
            id="street"
            class="info-block__field"
            v-model.trim="street"
          />
        </div>
        <div class="info-block__item">
          <label for="house" class="info-block__label">Дом</label>
          <input
            type="text"
            id="house"
            @input="setHouse"
            class="info-block__field info-block__field_short"
          />
        </div>
        <div class="info-block__item">
          <label for="index" class="info-block__label">Индекс</label>
          <input
            type="text"
            id="index"
            @input="setIndex"
            class="info-block__field info-block__field_short"
          />
        </div>
      </div>
      <div class="info-block">
        <h3 class="info-block__title">Паспорт</h3>
        <div class="info-block__item">
          <label for="doctor" class="info-block__label">Тип документа*</label>
          <select
            id="doctor"
            class="info-block__field info-block__field_select"
            :class="{ 'block-error': $v.docType.$error }"
            @change="setDocType"
          >
            <option hidden disabled selected value="">
              Выберите из списка
            </option>
            <option value="Pasport">Паспорт</option>
            <option value="Birth certificate">Свидетельство о рождении</option>
            <option value="Driver's license">Вод. удостоверение</option>
          </select>
          <div class="error" v-if="$v.docType.$error">
            Поле обязательно для заполнения
          </div>
        </div>
        <div class="info-block__item">
          <label for="issued" class="info-block__label">Кем выдан</label>
          <input
            type="text"
            id="issued"
            class="info-block__field"
            v-model.trim="issuedBy"
          />
        </div>
        <div class="info-block__item">
          <label for="series" class="info-block__label">Серия</label>
          <input
            type="text"
            id="series"
            @input="setSeries"
            class="info-block__field info-block__field_short"
          />
        </div>
        <div class="info-block__item">
          <label for="number" class="info-block__label">Номер</label>
          <input
            type="text"
            id="number"
            @input="setNumber"
            class="info-block__field info-block__field_short"
          />
        </div>
        <div class="info-block__item info-block__item_date">
          <label for="date" class="info-block__label">Дата выдачи*</label>
          <input
            type="date"
            id="date"
            class="info-block__field"
            @input="$v.issuedDate.$touch"
            :class="{ 'block-error': $v.issuedDate.$error }"
            v-model="issuedDate"
          />
          <div class="error" v-if="$v.issuedDate.$error">
            Поле обязательно для заполнения
          </div>
        </div>
      </div>
      <p class="form-hint">*Поле обязательное для заполнения.</p>
      <button type="submit" class="form__btn">Создать клиента</button>
    </form>
  </div>
</template>

<script>
import { required } from 'vuelidate/lib/validators';
import Modal from './Modal';

export default {
  name: 'HelloWorld',
  components:{  
    Modal
  },
  data() {
    return {
      showModal: false,
      name: '',
      surname: '',
      patronymic: '',
      birthdate: '',
      phone: '',
      gender: '',
      clientGroupe: '',
      doctor: '',
      sendMsg: true,
      index: '',
      country: '',
      region: '',
      city: '',
      street: '',
      house: '',
      docType: '',
      series: '',
      number: '',
      issuedBy: '',
      issuedDate: '',
    };
  },
  validations: {
    name: {
      required,
    },
    surname: {
      required,
    },
    birthdate: {
      required,
    },
    phone: {
      required,
    },
    clientGroupe: {
      required,
    },
    city: {
      required,
    },
    docType: {
      required,
    },
    issuedDate: {
      required,
    }
  },
  methods: {
    onSubmit(e) {
      this.$v.$touch();
      if (!this.$v.$anyError) {
        this.showModal = true;
        this.clearData();
        e.target.reset();
      }
    },
    clearData(){
      this.$v.$reset();
      this.name = '';
      this.surname = '';
      this.patronymic = '';
      this.birthdate = '';
      this.phone = '';
      this.gender = '';
      this.clientGroupe = '';
      this.doctor = '';
      this.sendMsg = true;
      this.index = '';
      this.country = '';
      this.region = '';
      this.city = '';
      this.street = '';
      this.house = '';
      this.docType = '';
      this.series = '';
      this.number = '';
      this.issuedBy = '';
      this.issuedDate = '';
    },
    phoneMask(e) {
      const value = e.target.value;
      const template = '+7 (___) ___-__-__';
      const def = template.replace(/\D/g, '');
      const val = value.replace(/\D/g, '');
      let i = 0;
      let newValue = template.replace(/[_\d]/g, function (a) {
        return i < val.length ? val.charAt(i++) || def.charAt(i) : a;
      });
      i = newValue.indexOf('_');
      if (i != -1) {
        newValue = newValue.slice(0, i);
      }
      let reg = template
        .substr(0, value.length)
        .replace(/_+/g, function (a) {
          return '\\d{1,' + a.length + '}';
        })
        .replace(/[+()]/g, '\\$&');
      reg = new RegExp('^' + reg + '$');
      if (reg.test(value) || value.length < 5) {
        if (newValue[1] != '7') {
          newValue = newValue.replace(newValue[1], '7');
        }
        this.phone = newValue;
      }
      if (e.type == 'blur' && value.length < 5) {
        this.phone = '';
      }
      this.$v.phone.$touch();
    },
    setDocType(e) {
      this.docType = e.target.value;
    },
    setSeries(e) {
      this.series = e.target.value.replace(/[^\d]/g, '').substr(0, 4);
      e.target.value = this.series;
    },
    setNumber(e) {
      this.number = e.target.value.replace(/[^\d]/g, '').substr(0, 6);
      e.target.value = this.number;
    },
    setHouse(e) {
      this.house = e.target.value.replace(/[^\d]/g, '');
      e.target.value = this.house;
    },
    setIndex(e) {
      this.index = e.target.value.replace(/[^\d]/g, '').substr(0, 6);
      e.target.value = this.index;
    },
    setDoctor(e) {
      this.doctor = e.target.value;
    },
    setClientGroupe(e) {
      if (this.clientGroupe.length === 0) {
        this.clientGroupe = e.target.value;
      } else {
        if (this.clientGroupe.includes(e.target.value)) {
          const firstIndex = this.clientGroupe.indexOf(e.target.value);
          let secondIndex = this.clientGroupe.slice(firstIndex).indexOf(',');
          if (secondIndex > 0) {
            secondIndex += this.clientGroupe.slice(0, firstIndex).length;
            if (firstIndex - 2 < 0) {
              this.clientGroupe = this.clientGroupe.slice(secondIndex + 2);
            } else {
              this.clientGroupe =
                this.clientGroupe.slice(0, firstIndex - 2) +
                this.clientGroupe.slice(secondIndex);
            }
          } else {
            if (firstIndex - 2 < 0) {
              this.clientGroupe = '';
            } else {
              this.clientGroupe = this.clientGroupe.slice(0, firstIndex - 2);
            }
          }
        } else {
          this.clientGroupe += ', ' + e.target.value;
        }
      }
      e.target.value = '';
      this.$v.clientGroupe.$touch();
    },
  },
};
</script>

<style scoped lang="scss">
/*
#1ab188 - button
#90979c - placeHolderText/borders
#435159 - notactive
#ffffff - textColor
*/

.main {
  width: 100%;
  display: flex;
  justify-content: center;
}

.form {
  display: flex;
  align-items: center;
  flex-direction: column;
  width: 50%;
  padding: 2rem;
  box-sizing: border-box;
  border: 1px solid #90979c;
  border-radius: 0.5rem;
  background: #24313c;
  color: #ffffff;

  .info-block {
    display: flex;
    flex-wrap: wrap;
    margin-bottom: 2rem;
    width: 100%;

    // &:last-child {
    //   margin: 0;
    // }

    .info-block__title {
      margin-top: 0;
      letter-spacing: 0.08rem;
      font-size: 1.5rem;
      font-weight: 600;
      width: 100%;
    }

    .info-block__item {
      position: relative;
      display: flex;
      flex-direction: column;
      margin-bottom: 1.5rem;
      width: 50%;

      .info-block__field_select {
        padding: 0 0.25rem;
        cursor: pointer;
      }

      .info-block__item__gender {
        display: flex;
        font-size: 0.9rem;
        margin-top: 0.2rem;

        .info-block__field {
          width: auto;
          height: auto;
          cursor: pointer;
          margin-left: 0.75rem;

          &:first-child {
            margin-left: 0;
          }
        }
      }
    }

    .info-block__label {
      width: fit-content;
      margin: 0;
    }

    .info-block__field {
      padding: 0 0.5rem;
      margin-top: 0.2rem;
      width: 80%;
      height: 1.75rem;
      background: #435159;
      color: #fff;
      box-sizing: border-box;
      border-width: 2px;
      border-style: inset;
      border-color: rgb(110, 110, 110);
      font: {
        family: 'Roboto';
        size: 0.9rem;
        weight: 400;
      }

      &:focus {
        outline: none;
        border-color: rgb(66, 138, 57);
      }
    }
    
    .info-block__chevron {
      position: absolute;
      z-index: 1;
      right: 22%;
      bottom: 9%;

      path {
        fill: #fff;
      }
    }

    .block-error {
      border-color: #9f2a2a !important;
      background: rgba(255, 20, 20, 0.5);
    }

    .info-block__item_date {
      ::-webkit-calendar-picker-indicator {
        color: transparent;
        opacity: 1;
        background: url('../assets/calendar.svg') no-repeat center;
        background-size: contain;
        cursor: pointer;
      }
    }

    .info-block__item_multiple {
      .info-block__field {
        padding-right: 1.5rem;
      }

      .info-block__field_select {
        position: absolute;
        padding: 0 0.5rem;
        bottom: 0;
        left: 0;
        opacity: 0;
        z-index: 2;
      }

      .info-block__field_select:focus + .info-block__field {
        border-color: rgb(66, 138, 57);
      }
    }

    .info-block__item_checkbox {
      flex-direction: row;
      align-items: center;

      .info-block__field {
        margin: 0;
        margin-right: 0.5rem;
        width: auto;
        height: auto;
        cursor: pointer;
      }

      .info-block__label {
        font-size: 0.9rem;
      }
    }

    .info-block__field_short {
      width: 40%;
    }
  }

  .form__btn {
    font-family: 'Roboto';
    font-size: 1rem;
    color: #fff;
    background: #1ab188;
    width: 30%;
    height: 2.5rem;
    border: 1px solid #90979c;
    border-radius: 1rem;
    cursor: pointer;

    &:hover {
      background: #189a78;
    }

    &:active {
      background: #1dc296;
    }

    &:disabled {
      background: #435159;
    }
  }

  .form-hint {
    width: 100%;
    font-size: 0.8rem;
    font-style: italic;
    margin-top: 0;
    letter-spacing: 0.04rem;
  }

  .error {
    color: #ff0404;
    font-size: 0.75rem;
    position: absolute;
    bottom: -1rem;
  }
}
</style>
