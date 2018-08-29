<template>
  <div id="app">
    <app-navbar/>
    <user-form/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import AppNavbar from './components/AppNavbar.vue'
import UserForm from './components/UserForm.vue'
export default {
  name: 'app',
  components: {
    HelloWorld,
    AppNavbar,
    UserForm
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Francois+One');
</style>
