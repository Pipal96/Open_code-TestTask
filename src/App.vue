<template>
  <div id="app">
    <app-main></app-main>
  </div>
</template>

<script>
  import Main from './components/Main'

  export default {
    name: 'App',
    components: {
      'app-main': Main,
    }
  }
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');

  * {
    font-family: 'Roboto', sans-serif;
    box-sizing: border-box;
  }

  #app {
    padding: 55px;
    box-sizing: border-box;

    /* COLOR */
    --app-background-color: #E5E5E5;
    --black-color: #000;
    --background-dropdown-button: #D9D9D9;
    --border-color: #999999;
    --white-color: #fff;
    --green-fill: rgb(9, 126, 9);
    --red-fill: red;

    /* SIZE */
    --height-tabel: 100%;
    --height-dropdown-item: 45px;
    --width-dropdown-item: 335px;
  }

  fieldset {
    border: none;
  }
</style>