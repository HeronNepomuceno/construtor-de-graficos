<template>
  <div class="container">
    <header-comp></header-comp>
    <form-comp></form-comp>
  </div>
</template>

<script>
  import HeaderComp from './components/HeaderComp';
  import FormComp from './components/FormComp.vue';

  export default {
    name: 'App',
    components: {
      HeaderComp,
      FormComp
    }
  };
</script>

<style>
  @import './assets/css/variables.css';
  @import './assets/css/reset.css';
  @import url('https://fonts.googleapis.com/css2?family=Oxygen:wght@300;400;700&display=swap');

  .container {
    height: 100%;
    width: 100%;
  }
</style>

