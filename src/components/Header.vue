<template>
 <header id="header">
     <nav class="nav-menu" :class="{'active':fixedMenu}">
         <div class="container flex-container">
             <div class="logo">
                 <a href="#"><img src="../assets/logo/logo.svg" alt="logo"></a>
             </div>
             <ul class="menu flex-container">
                 <li class="menu-item" v-for="(menuItem,index) in menu" :key="index"><a :href="menuItem.url">{{menuItem.pageName}}</a></li>
             </ul>
             <div class="login-container flex-container">
                 <div class="login-contact">
                 <span class="login-name">
                   {{currentUser.name}}
                 </span>
                     <span class="login-email">
                   {{currentUser.email}}
                 </span>
                 </div>
                 <div class="login-avatar">
                     <a href="#"><img :src="currentUser.photo" alt="login"></a>
                 </div>
                 <a href="#" class="logout">
                 </a>
             </div>
             <button class="toggle-button" @click="activeMenu">
                 <span class="icon-bar"></span>
                 <span class="icon-bar"></span>
                 <span class="icon-bar"></span>
             </button>
         </div>
     </nav>
     <div class="toggle-menu">
         <div class="mobile-header">
             <div class="mobile-login container">
                 <div class="login-avatar">
                     <a href="#"><img :src="currentUser.photo" alt="login"></a>
                 </div>
                 <span class="login-name">
                   {{currentUser.name}}
                 </span>
                 <span class="login-email">
                   {{currentUser.email}}
                 </span>
             </div>
             <hr>
             <ul class="mobile-menu container">
                 <li class="mobile-menu-item" v-for="(menuItem,index) in menu" :key="index"><a :href="menuItem.url">{{menuItem.pageName}}</a></li>
             </ul>
         </div>
         <div class="mobile-background" @click="disableMenu"></div>
     </div>
 </header>
</template>
<script>
    import axios from 'axios'
    export default {
        data(){
            return {
                menu: [
                    {url: '#Aboutme',pageName: 'About me'},
                    {url: '#Relationship',pageName: 'Relationships'},
                    {url: '#Requirements',pageName: 'Requirements'},
                    {url: '#Users',pageName: 'Users'},
                    {url: '#SignUp',pageName: 'Sign Up'}
                ],
                currentUser: {
                    name: '',
                    photo: '',
                    email: ''
                },
                fixedMenu: false
            }
        },
        created() {
           // Получаем текущего пользователя
           axios({
               methods: 'get',
               url: 'https://frontend-test-assignment-api.abz.agency/api/v1/users/1'
           })
               .then(response =>{
                   this.currentUser.name = response.data.user.name;
                   this.currentUser.email = response.data.user.email;
                   this.currentUser.photo = response.data.user.photo;
               })
               .catch(error => {
                   console.log(error);
               })
        },
        mounted(){
             this.scrollCheck();
          },
        methods: {
            scrollCheck: function(){
                window.addEventListener('scroll',()=>{
                    if(window.pageYOffset>1){
                        this.fixedMenu = true;
                    }else{
                        this.fixedMenu = false;
                    }
                })
            },
            activeMenu: function () {
                function activateMenu(item){
                    document.querySelector(item).classList.add('active');
                }
                activateMenu('.toggle-button');
                activateMenu('.toggle-menu');
            },
            disableMenu: function () {
                function disabledMenu(item){
                    document.querySelector(item).classList.remove('active');
                }
                disabledMenu('.toggle-button');
                disabledMenu('.toggle-menu');
            }
        }
    }
</script>
