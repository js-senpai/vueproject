<template>
  <div id="app">
     <header-template></header-template>
     <banner></banner>
  </div>
</template>
<style lang="sass">
@import './sass/main.sass'
</style>
<script>
import Header from './components/Header'
import Banner from './components/Banner'
export default{
  name: 'app',
  data(){
    return {

    }
  },
  components:{
    'header-template':Header,
    'banner': Banner
  }
}
</script>
