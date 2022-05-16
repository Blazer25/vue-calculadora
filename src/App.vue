<template>
  <div id="app">
      <Calculadora />
    <router-view/>
  </div>
</template>

<script>
import Calculadora from './views/HomeView.vue'
export default {
  name: 'app',
  components:{
    Calculadora
  }
}
</script>


<style>
body{
  background: #000000;  /* fallback for old browsers */
  background: -webkit-linear-gradient(to right, #434343, #000000);  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to right, #434343, #000000); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}
</style>
