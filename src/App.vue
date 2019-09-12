<template>
  <div id="app">
     <header-template></header-template>
     <banner></banner>
     <about></about>
     <requirements></requirements>
     <users></users>
     <registration></registration>
     <footer-template></footer-template>
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
import Users from "./components/Users";
import Registration from "./components/Registration";
import Footer from "./components/Footer";
export default{
  name: 'app',
  data(){
    return {

    }
  },
  mounted(){
      const anchors = document.querySelectorAll('a[href*="#"]')
      for (let anchor of anchors) {
          anchor.addEventListener('click', function (e) {
              e.preventDefault();
              const blockID = anchor.getAttribute('href').substr(1);
              document.getElementById(blockID).scrollIntoView({
                  behavior: 'smooth',
                  block: 'start'
              })
          })
      }
  },
  components:{
    'header-template':Header,
    'banner': Banner,
    'about': About,
    'requirements': Requirements,
    'users': Users,
    'registration': Registration,
    'footer-template': Footer
  }
}

</script>
