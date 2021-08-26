<template>
  <div class="main">
    <b-container fluid>
      <b-row class="my-1" v-for="type in types" :key="type">
        <b-col sm="3">
          <label :for="`type-${type}`"
            ><code>{{ type }}</code
            >:</label
          >
        </b-col>
        <b-col sm="9">
          <b-form-input :id="`type-${type}`" :type="type"></b-form-input>
        </b-col>
      </b-row>
    </b-container>
    <div>
      <b-row class="my-1">
        <b-col sm="9">
          <label><code>Страна проживания</code>:</label>
          <b-form-select
            v-model="selected"
            :options="countries"
          ></b-form-select>
        </b-col>
      </b-row>
      <b-row class="my-1">
        <b-col>
          <label><code>Любимые темы</code>:</label>
          <b-form-select v-model="selected" :options="themes"></b-form-select>
        </b-col>
      </b-row>
    </div>
  </div>
</template>

<script>
export default {
  name: "myForm",
  data() {
    return {
      selected: null,
      types: ["Логин", "Почта", "Пароль"],
      countries: [
        { text: "Россия" },
        { text: "Англия" },
        { text: "Америка" },
        { text: "Китай" },
        { text: "Франция" },
      ],
      themes: [
        { text: "IT" },
        { text: "Юмор" },
        { text: "Фильмы" },
        { text: "Игры" },
        { text: "Литература" },
      ],
    };
  },
};
</script>

<style scoped>
.main {
  margin-top: 20px;
}

div {
  width: 600px;
  margin-left: auto;
  margin-right: auto;
}
</style>