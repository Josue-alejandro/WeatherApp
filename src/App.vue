<template>
  <div class="container">
    <panel-component></panel-component>
  </div>
</template>

<script>
import PanelComponent from './components/PanelComponent.vue';

export default {
  components:{
    PanelComponent
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300&display=swap');

body{
  background-image: url(assets/background.jpg);
  background-position: center center;
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: cover;
  background-color: rgba(0,177,214,1);
  font-family: 'Roboto', sans-serif;
}

.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
</style>