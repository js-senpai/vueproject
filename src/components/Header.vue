<template>
 <nav class="nav-menu">
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
     </div>
 </nav>
</template>
<script>
    import axios from 'axios'
    export default {
        data(){
            return {
                menu: [
                    {url: '#',pageName: 'About me'},
                    {url: '#',pageName: 'Relationships'},
                    {url: '#',pageName: 'Requirements'},
                    {url: '#',pageName: 'Users'},
                    {url: '#',pageName: 'Sign Up'}
                ],
                currentUser: {
                    name: '',
                    photo: '',
                    email: ''
                }
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
               .catch(e => {
                   console.log(e)
               })
        }
    }
</script>