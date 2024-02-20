<template>
  <div id="app">
    <TheHeader />
    <LoanForm />
  </div>
</template>

<script>
import TheHeader from './components/TheHeader.vue'
import LoanForm from './components/LoanForm.vue'

export default {
  name: 'App',
  components: {
    TheHeader,
    LoanForm
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #EF6C00;
  margin-top: 60px;
}
</style>
