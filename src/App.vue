<script>
import HeaderComp from '@/components/Header.vue'
import MainComp from '@/components/Main.vue'
import FooterMod from '@/components/Footer.vue'
export default {
  components: {HeaderComp,MainComp,FooterMod}
}
</script>

<template>
   <v-app>
     <HeaderComp></HeaderComp>
     <MainComp></MainComp>
     <FooterMod></FooterMod>
   </v-app>
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
