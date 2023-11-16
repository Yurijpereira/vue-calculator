<template>
  <div class="appContainer">
    <h1 class="title">Calculator</h1>
    <Calculator class="calculator"/>
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue';

export default {
  name: 'App',
  components: {
    Calculator
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}

body{
  background-color: #0e0d0d;
}

.appContainer {
  margin: 0 auto;
}

.title {
  color: #ce5746;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 20px auto;
}

.calculator {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
}

#app {
  font-family: Arial, Helvetica, sans-serif;
  margin-top: 50px;
}
</style>
