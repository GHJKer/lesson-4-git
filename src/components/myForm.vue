<template>
  <form class="sign-up" @submit.prevent="checkForm">
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
        Email некорректный
      </p>
    </div>
    <div class="form-group">
      <label for="password">Пароль:</label>
      <input 
        id="password" 
        class="form-control"
        v-model.trim="form.password"
      >
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
      <select id="themes" class="form-control" v-model="form.favouriteThemes" multiple>
        <option
        v-for="(theme, index) in themes"
        :value="theme.value"
        :key="index"
        >{{ theme.label }}</option>
      </select>
    </div>
    <div class="form-group form-check">
      <input type="checkbox" value="1" class="form-check-input" id="notification" v-model="form.mailing">
      <label for="notification" class="form-check-label">Уведомлять меня о новых курсах</label>
    </div>
    <div class="form-group form-check">
      <input type="checkbox" value="2" class="form-check-input" id="notification" v-model="form.mailing">
      <label for="notification" class="form-check-label">Уведомлять меня о новых курсах 2</label>
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
</template>

<script>
import { validationMixin } from 'vuelidate'
import { required, minLength, email } from 'vuelidate/lib/validators'

export default {
  name: "myForm",
  mixins: [validationMixin],
  data() {
    return {
      form: {
        password: '',
        email: '',
        login: '',
        country: 'Russia',
        mailing: [],
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
      ]
    };
  },
  validations: {
    form: {
      login: {required, minLength: minLength(5)},
      password: {required, email},
      email: {required}
    }
  },
  methods: {
    checkForm () {
      this.$v.form.$touch()
      if (!this.$v.form.$error) {
        console.log('Валидация прошла успешно')
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

button {
  margin-top: 15px;
}
</style>