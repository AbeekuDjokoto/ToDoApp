<template>
  <div class="container">
    <app-home></app-home>
  </div>
</template>

<script>
import HomeVue from './views/Home.vue'
export default {
  components:{
    "app-home": HomeVue
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
}

html, body{
  max-width: 100%;
  overflow-x: hidden;
}

#app {
  font-family: 'Josefin Sans', sans-serif;
}

</style>
