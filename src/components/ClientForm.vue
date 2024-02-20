<template>
  <form class="signup" @submit.prevent="checkForm">
    <div class="user-main-info">
      <div class="form-group">
        <label for="second-name">Фамилия:</label>
        <input type="text" id="second-name" v-model="form.secondName" :class="$v.form.secondName.$error ? 'invalid' : ''"/>
        <p
          v-if="$v.form.secondName.$dirty && !$v.form.secondName.required"
          class="invalid-feedback"
        >
          Обязательное поле
        </p>
      </div>
      <div class="form-group">
        <label for="name">Имя:</label>
        <input type="text" id="name" v-model="form.name" :class="$v.form.name.$error ? 'invalid' : ''"/>
        <p
          v-if="$v.form.name.$dirty && !$v.form.name.required"
          class="invalid-feedback"
        >
          Обязательное поле
        </p>
      </div>
      <div class="form-group">
        <label for="middle-name">Отчество:</label>
        <input type="text" id="middle-name" v-model="form.middleName" />
      </div>
      <div class="form-group">
        <label for="birthday">Дата рождения:</label>
        <input type="date" id="birthday" v-model="form.birthday" :class="$v.form.birthday.$error ? 'invalid' : ''"/>
        <p
          v-if="$v.form.birthday.$dirty && !$v.form.birthday.required"
          class="invalid-feedback"
        >
          Обязательное поле
        </p>
      </div>
      <div class="form-group">
        <label for="phone">Номер телефона:</label>
        <input type="tel" id="phone" v-model="form.phone" :class="$v.form.phone.$error ? 'invalid' : ''" />
        <p
          v-if="$v.form.phone.$dirty && !$v.form.phone.required"
          class="invalid-feedback"
        >
          Обязательное поле
        </p>
        <p
          v-if="$v.form.phone.$dirty &&  !$v.form.phone.numeric && !$v.form.phone.validator"
          class="invalid-feedback"
        >
          Ошибка! Должно быть 11 цифр и начинаться с 7
        </p>
      </div>
      <div class="form-group">
        <label>Пол:</label>
        <div>
          <input
            type="radio"
            id="male"
            value="male"
            name="sex"
            v-model="form.sex"
          />
          <label for="male">Мужской</label>
        </div>
        <div>
          <input
            type="radio"
            id="female"
            value="female"
            name="sex"
            v-model="form.sex"
          />
          <label for="female">Женский</label>
        </div>
      </div>
      <div class="form-group">
        <label for="clientsGroups" style="text-align: left"
          >Группа клиентов</label
        >
        <div class="select select--multiple">
          <select id="clientsGroups" multiple v-model="form.clientsGroups" :class="$v.form.clientsGroups.$error ? 'invalid' : ''">
            <option
              v-for="(item, key) in clientsGroups"
              :key="key"
              :value="item"
            >
              {{ item }}
            </option>
          </select>
          <span class="focus"></span>
        </div>
        <p
          v-if="$v.form.clientsGroups.$dirty && !$v.form.clientsGroups.required"
          class="invalid-feedback"
        >
          Обязательное поле
        </p>
      </div>
      <div class="form-group">
        <label for="doctors" style="text-align: left; margin-top: 0"
          >Лечащий врач:
        </label>
        <div class="select">
          <select id="doctors" v-model="form.doctor">
            <option v-for="(doctor, key) in doctors" :key="key" :value="doctor">
              {{ doctor }}
            </option>
          </select>
          <span class="focus"></span>
        </div>
      </div>
      <div class="form-group">
        <div>
          <input
            type="checkbox"
            id="sms"
            v-model="form.sms"
            style="margin: 0.4rem"
          />
          <label for="sms">SMS-Оповещение</label>
        </div>
      </div>
    </div>
    <div>
      <div class="user-passport">
        <div class="form-group">
          <label for="documentType" style="text-align: left; margin-top: 0"
            >Тип Документа:
          </label>
          <div class="select">
            <select id="doctors" v-model="form.documentType" :class="$v.form.documentType.$error ? 'invalid' : ''">
              <option
                v-for="(doc, key) in documentType"
                :key="key"
                :value="doc"
              >
                {{ doc }}
              </option>
            </select>
            <span class="focus"></span>
          </div>
          <p
          v-if="$v.form.documentType.$dirty && !$v.form.documentType.required"
          class="invalid-feedback"
        >
          Обязательное поле
        </p>
        </div>
        <div class="form-group">
          <label for="passportSeries">Серия:</label>
          <input
            type="text"
            id="passportSeries"
            v-model="form.passportSeries"
          />
        </div>
        <div class="form-group">
          <label for="passportNumber">Номер:</label>
          <input
            type="text"
            id="passportNumber"
            v-model="form.passportNumber"
          />
        </div>
        <div class="form-group">
          <label for="passportBy">Кем выдан:</label>
          <input type="text" id="passportBy" v-model="form.passportBy" />
        </div>
        <div class="form-group">
          <label for="passportDate">Дата выдачи:</label>
          <input type="date" id="passportDate" v-model="form.passportDate" :class="$v.form.secondName.$error ? 'invalid' : ''" />
          <p
          v-if="$v.form.passportDate.$dirty && !$v.form.passportDate.required"
          class="invalid-feedback"
        >
          Обязательное поле
        </p>
        </div>
      </div>
      <div class="user-address">
        <div class="form-group">
          <label for="indexx">Индекс:</label>
          <input type="text" id="index" v-model="form.address.index" />
        </div>
        <div class="form-group">
          <label for="country">Страна:</label>
          <input type="text" id="country" v-model="form.address.country" />
        </div>
        <div class="form-group">
          <label for="state">Область:</label>
          <input type="text" id="state" v-model="form.address.state" />
        </div>
        <div class="form-group">
          <label for="city">Город:</label>
          <input type="text" id="city" v-model="form.address.city"  :class="$v.form.secondName.$error ? 'invalid' : ''"/>
          <p
          v-if="$v.form.address.city.$dirty && !$v.form.address.city.required"
          class="invalid-feedback"
        >
          Обязательное поле
        </p>
        </div>
        <div class="form-group">
          <label for="street">Улица:</label>
          <input type="text" id="street" v-model="form.address.street" />
        </div>
        <div class="form-group">
          <label for="house">Дом:</label>
          <input type="text" id="house" v-model="form.address.house" />
        </div>
      </div>
      <button type="submit" class="btn">Сохранить</button>
    </div>
  </form>
</template>

<script>
import { validationMixin } from "vuelidate";
import { required, numeric} from "vuelidate/lib/validators";

export default {
  name: "ClientForm",
  mixins: [validationMixin],
  data() {
    return {
      form: {
        name: "",
        secondName: "",
        middleName: "",
        birthday: "",
        phone: "",
        sex: "male",
        clientsGroups: [],
        doctor: "Иванов",
        sms: true,
        documentType: "Паспорт",
        passportSeries: "",
        passportNumber: "",
        passportBy: "",
        passportDate: "",
        address: {},
      },
      clientsGroups: ["VIP", "Проблемные", "ОМС"],
      doctors: ["Иванов", "Захаров", "Чернышева"],
      documentType: [
        "Паспорт",
        "Свидетельство о рождении",
        "Вод. удостоверение",
      ],
    };
  },
  validations: {
    form: {
      secondName: { required },
      name: { required },
      birthday: { required },
      phone: {
        required,
        numeric,
        validator(value) {
          return !(value.at(0) === 7 && value.length === 11)
        },
      },
      clientsGroups: {required},
      address: {
        city: {required}
      },
      documentType: {required},
      passportDate: {required}
    },
  },
  methods:{
    checkForm() {
      this.$v.form.$touch()
      if (!this.$v.form.$error) {
        alert('Новый клиент успешно создан')
      }
    },

  }
};
</script>

<style lang="sass" scoped>
@import "../styles/select-styling.sass"
.signup
    width: 100%
    max-width: 1200px
    margin: 0 auto
    display: flex
    gap: 15px

.user-main-info
  display: flex
  flex-wrap: wrap
  flex-direction: column
  max-width: 600px
  width: 100%
  margin: 0 auto
  gap: 15px
.user-passport
  display: flex
  flex-wrap: wrap
  flex-direction: column
  max-width: 600px
  width: 100%
  margin: 0 auto
  gap: 15px
.user-address
    display: flex
    flex-wrap: wrap
    max-width: 1200px
    gap: 15px
    margin-top:25px

    .form-group
        width: auto
.form-group
  width: 100%
  display: flex
  flex-direction: column
  max-width: 600px
  gap: 5px
  text-align: left
input
  margin-left: 0
  border: 2px solid #000000
  height: 24px
  border-radius: 4px

.invalid
    border-color: red
    color: red
.invalid-feedback
    color: red

.btn
    margin-top: 24px
    background-color: blue
    border: none
    color: white
    padding: 15px 32px
    text-align: center
    text-decoration: none
    display: inline-block
    font-size: 16px
</style>
