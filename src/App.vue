<template>
  <div id="app">
     <header-template></header-template>
  </div>
</template>
<style lang="sass">
@import './sass/main.sass'
</style>
<script>
import Header from './components/Header'
export default{
  name: 'app',
  data(){
    return {

    }
  },
  components:{
    'header-template':Header
  }
}
</script>
