<script>
import HeaderComp from '@/components/Header.vue'
import MainComp from '@/components/Main.vue'

export default {
  components: {HeaderComp,MainComp}
}
</script>

<template>
  <HeaderComp></HeaderComp>
  <MainComp></MainComp>
  
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

}
</style>
