<template>
  <div class="jumbotron">
    <Navbar />
    <router-view />
  </div>
</template>

<script>
import Navbar from './componentes/Navbar'

export default {
  name: 'App',
  components: {
    Navbar
  }
}
</script>

<style>
  .jumbotron{
  } 
</style>
