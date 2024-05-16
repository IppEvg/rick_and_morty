<script>
import HeaderComp from '@/components/Header.vue';
import MainComp from '@/components/Main.vue'
export default {
  components: {HeaderComp,MainComp}
}
</script>

<template>
  <HeaderComp></HeaderComp>
  <MainComp></MainComp>
  <v-pagination :length="6"></v-pagination>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
