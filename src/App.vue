<template>
  <div id="app">
     <header-template></header-template>
     <banner></banner>
     <about></about>
     <requirements></requirements>
  </div>
</template>
<style lang="sass">
@import './sass/main.sass'
</style>
<script>
import Header from './components/Header';
import Banner from './components/Banner';
import About from './components/About';
import Requirements from "./components/Requirements";
export default{
  name: 'app',
  data(){
    return {

    }
  },
  components:{
    'header-template':Header,
    'banner': Banner,
    'about': About,
    'requirements': Requirements
  }
}
</script>
