<template>
  <div id="app">
    <myForm />
  </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

import myForm from './components/myForm.vue'

export default {
  name: 'App',
  components: {
    myForm
  }
}
</script>