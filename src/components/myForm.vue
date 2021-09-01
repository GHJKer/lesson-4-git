<template>
  <div>
    <form class="sign-up" v-if="!registrationPassed" @submit.prevent="checkForm">
    <div class="form-group">
      <label for="login">Логин:</label>
      <input 
        id="login" 
        class="form-control"
        :class="$v.form.login.$error ? 'is-invalid' : ''"
        v-model.trim="form.login"
      >
      <p v-if="$v.form.login.$dirty && !$v.form.login.required" class="invalid-feedback">
        Обязательное поле
      </p>
      <p v-if="$v.form.login.$dirty && !$v.form.login.minLength" class="invalid-feedback">
        Здесь должно быть больше 5-ти символов
      </p>
    </div>
    <div class="form-group">
      <label for="email">Почта:</label>
      <input 
        id="email" 
        class="form-control"
        :class="$v.form.email.$error ? 'is-invalid' : ''"
        v-model.trim="form.email"
      >
      <p v-if="$v.form.login.$dirty && !$v.form.email.required" class="invalid-feedback">
        Обязательное поле
      </p>
      <p v-if="$v.form.login.$dirty && !$v.form.email.email" class="invalid-feedback">
        Email некорректный!
      </p>
    </div>
    <div class="form-group">
      <label for="password">Пароль:</label>
      <input 
        id="password" 
        class="form-control"
        :class="$v.form.password.$error ? 'is-invalid' : ''"
        v-model.trim="form.password"
      >
      <p v-if="$v.form.login.$dirty && !$v.form.password.required" class="invalid-feedback">
        Обязательное поле
      </p>
    </div>
    <div class="from-group">
      <label for="country">Страна проживания:</label>
      <select id="country" class="form-control" v-model="form.country">
        <option 
        v-for="(country, index) in countries"
        :value="country.value"
        :key="index"
        >{{ country.label }}</option>
      </select>
    </div>
    <div class="from-group">
      <label for="themes">Любимые темы:</label>
      <select id="themes" 
      class="form-control" 
      :class="$v.form.favouriteThemes.$error ? 'is-invalid' : ''"
      v-model="form.favouriteThemes" multiple>
        <option
        v-for="(theme, index) in themes"
        :value="theme.value"
        :key="index"
        >{{ theme.label }}</option>
      </select>
      <p v-if="$v.form.login.$dirty && !$v.form.favouriteThemes.maxLength" class="invalid-feedback">
        Не более 3-х тем!
      </p>
    </div>
    <div class="form-group form-check">
      <input type="checkbox" value="1" class="form-check-input" id="notification" v-model="form.mailing">
      <label for="notification" class="form-check-label">Уведомлять меня о новых курсах</label>
    </div>
    <div class="form-group form-check">
      <input type="checkbox" value="2" class="form-check-input" id="notification" 
      v-model="form.agreeWithRules">
      <label for="notification" :class="$v.form.agreeWithRules.$error ? 'is-invalid' : ''" class="form-check-label">Ознакомлен с правилами</label>
      <p v-if="$v.form.login.$dirty && !$v.form.agreeWithRules.required" class="invalid-feedback">
        Ознакомтесь с правилами!
      </p>
    </div>
    <div class="flex">
      <div class="form-check">
        <input type="radio" name="exampleRadios" id="male" class="form-check-input" value="male" v-model="form.gender">
        <label for="male" class="form-check-label">Мужчина</label>
      </div>
      <div class="form-check">
        <input type="radio" name="exampleRadios" id="female" class="form-check-input" value="female" v-model="form.gender">
        <label for="female" class="form-check-label">Женщина</label>
      </div>
    </div>
    <button type="submit" class="btn btn-primary">Сохранить</button>
  </form>
  <div v-else>
    <h1>{{ `${form.login}, поздравляем вы успешно прошли регистрацию` }}</h1>
  </div>
  </div>
</template>

<script>
import { validationMixin } from 'vuelidate'
import { required, minLength, maxLength, email } from 'vuelidate/lib/validators'

export default {
  name: "myForm",
  mixins: [validationMixin],
  data() {
    return {
      registrationPassed: false,
      form: {
        password: '',
        email: '',
        login: '',
        country: 'Russia',
        mailing: [],
        agreeWithRules: [],
        gender: 'male',
        favouriteThemes: [
          'IT'
        ]
      },
      countries: [
        {
          label: 'Россия',
          value: 'Russia'
        },
        {
          label: 'Япония',
          value: 'Japan'
        },
        {
          label: 'США',
          value: 'USA'
        },
      ],
      themes: [
        {
          label: 'Технологии',
          value: 'IT'
        },
        {
          label: 'Спорт',
          value: 'Sports'
        },
        {
          label: 'Кухня',
          value: 'Cuisine'
        },
        {
          label: 'Тачки',
          value: 'Cars'
        }
      ]
    };
  },
  validations: {
    form: {
      login: {required, minLength: minLength(5)},
      password: {required},
      email: {required, email},
      favouriteThemes: {maxLength: maxLength(3)},
      agreeWithRules: {required}
    }
  },
  methods: {
    checkForm () {
      this.$v.form.$touch()
      if (!this.$v.form.$error) {
        this.registrationPassed = true
      }
    }
  }
};
</script>

<style scoped>
.sign-up {
  width: 400px;
  margin-left: auto;
  margin-right: auto;
}

.main {
  margin-top: 20px;
}

.form-check {
  margin: 10px;
}

.flex {
  display: flex;
}

h1 {
  text-align: center
}

button {
  margin-top: 15px;
}
</style>