<template>
    <section class="contact-block container">
        <h2 class="contact-title" id="Users">Our cheerful users</h2>
        <h5 class="contact-subtitle">Attention! Sorting users by registration date</h5>
            <ul class="users-list flex-container">
                    <li class="users-item flex-container" v-if="user < users.length" v-for="(user,index) in usersToShow" :key="user">
                        <time class="registration-date" :datetime="users[user].registration_date | formatDate">{{users[user].registration_date | formatDate}}</time>
                        <div class="users-img"><img :src="users[user].photo" alt="user" class="lazy"></div>
                        <div class="users-info">
                            <h4 class="users-name">{{users[user].name}}</h4>
                            <span class="users-info-item user-position">{{users[user].position}}</span>
                            <span class="users-info-item user-email"><a :href="`mailto:${users[user].email}`">{{users[user].email}}</a></span>
                            <span class="users-info-item user-telephone"><a :href="`tel:${users[user].phone}`">{{users[user].phone}}</a></span>
                        </div>
                    </li>
            </ul>
            <button v-if="usersToShow < users.length" @click="usersToShow+=6" class="show-more">Show more</button>
    </section>
</template>
<script>
    import axios from 'axios'
    export default {
        data(){
            return {
                users:[].sort((prev, curr) => prev.registration_date - curr.registration_date),
                usersToShow: 6
            }
        },
        created() {
          //Получаем информацию о пользователях
          axios({
              methods: 'get',
              url: 'https://frontend-test-assignment-api.abz.agency/api/v1/users?count=100'
          }).then(response =>{
              console.log(response);
              for(let i = 0;i<response.data.users.length;i++){
                  this.users.push({registration_date:response.data.users[i].registration_timestamp,name:response.data.users[i].name,email:response.data.users[i].email,phone:response.data.users[i].phone,position:response.data.users[i].position,photo:response.data.users[i].photo})
              }
          })
          .catch(error =>{
            console.log(error);
           });
        },
        filters:{
            // Преобразовуем дату
            formatDate(value) {
                let currentDate = new Date(value*1000),
                fullDate = currentDate.toGMTString();
                return fullDate;
            }
        }
    }
</script>