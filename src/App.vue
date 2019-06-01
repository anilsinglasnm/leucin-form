<template>
  <div id="app">
    <AnalyticalMethodForm/>
  </div>
</template>

<script>
import AnalyticalMethodForm from './components/analyticalMethodForm/index'

export default {
  name: 'App',
  components: {
    AnalyticalMethodForm
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 5rem auto 0;
  width: 25rem;
}

label {
  display: block;
  margin: 0.5rem 0;
}
label::before {
  content: '*';
  color: red;
}
label > input, label > select, button {
  display: block;
  width: 100%;
  box-sizing: border-box;
}
button {
  margin: 0.5rem 0;
}
</style>
