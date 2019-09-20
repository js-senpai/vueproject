<template>
    <section class="registration-block container">
        <h2 class="registration-title" id="SignUp">Register to get a work</h2>
        <h5 class="registration-subtitle">Attention! After successful registration and alert, update the list of users in the block from the top</h5>
        <form action="POST" id="registration" @mouseover="checkValidate">
            <div class="registration-form flex-container">
                <div class="registration-item registration-text" :class="{'not-validate':validatorName}">
                    <input type="text" name="name" class="registration-input" placeholder="Your name"  required v-model.trim="newUser.name"  maxlength="15" :class="{'not-validate':validatorName,'validate':validateName}">
                    <span class="error-validation" :class="{'active':validatorName}">Error</span>
                </div>
                <div class="registration-item registration-email" :class="{'not-validate':validatorEmail}">
                    <input type="email" name="email" class="registration-input" placeholder="Your email" required v-model="newUser.email" maxlength="30" :class="{'not-validate':validatorEmail,'validate':validateEmail}">
                    <span class="error-validation" :class="{'active':validatorEmail}">Error</span>
                </div>
                <div class="registration-item registration-tel" :class="{'not-validate':validatorPhone}">
                    <input type="tel" name="phone" id="phone" class="registration-input" placeholder="+38(___) ___ __ __" required v-model.lazy="newUser.phone" :class="{'not-validate':validatorPhone,'validate':validatePhone}">
                    <span class="error-validation" :class="{'active':validatorPhone}">Error</span>
                </div>
                <div class="registration-item-bottom">
                    <div class="registration-item-bottom--select-position" :class="{'active': activeSelect,'not-validate':validatorSelect}">
                        <div class="selected-position flex-container">
                            <span class="selected-text">Select your position</span>
                            <span class="select-btn" @click="selectPosition" :class="{'active': activeSelect}"></span>
                        </div>
                        <div class="select-wrap">
                            <div class="select-items" v-for="(position,index) in positions" :key="index" @click="selectedPosition(position.position_name,position.position_id)">{{position.position_name}}</div>
                        </div>
                    </div>
                    <span class="error-validation" :class="{'active':validatorSelect}">Error</span>
                </div>
                <div class="registration-item-bottom">
                    <div class="registration-upload flex-container" :class="{'not-validate':validatorFile,'validate':validateFile}">
                        <span class="file-upload">Upload your photo</span>
                        <input type="file" name="file" id="file" class="registration-upload" required @change="onAttachmentChange" accept=".jpg, .jpeg">
                        <label for="file" class="subfile">Upload</label>
                    </div>
                    <span class="info-for-file" v-show="validatorFile==false">File format jpg  up to 5 MB, the minimum size of 70x70px</span>
                    <span class="error-validation" :class="{'active':validatorFile}">Error</span>
                </div>
            </div>
            <div class="fail-request" v-show="failRegistration"></div>
            <div class="successfull-registration" v-show="completeRegistration">Thank you for registration!</div>
            <input type="text" class="registration-submit" value="Sign Up" :class="{'disabled':activeValidate}" :disable="activeValidate" @click.prevent="submitRegistration">
        </form>
    </section>
</template>
<script>
    import axios from 'axios';
    import Inputmask from 'inputmask';
    export default {
        data(){
            return {
                token: '',
                positions: [],
                activeSelect: false,
                activeValidate: true,
                newUser:{
                    name: '',
                    photo: '',
                    email: '',
                    phone: '',
                    position: '',
                    position_id: ''
                },
                validatorName: false,
                validatorEmail: false,
                validatorSelect: null,
                validatorFile: false,
                validatorPhone: false,
                validateName: false,
                validateEmail: false,
                validateFile: false,
                validatePhone: false,
                completeRegistration: false,
                failRegistration: false
            }
        },
        watch:{
            // Валидация полей формы
            'newUser.name': function(value){
                if(value.length < 1 || value.length>60 || !value.match(/^[a-zA-ZА-Яа-яЁё\s-]+$/)){
                    this.validatorName = true;
                    this.validateName = false;
                }else{
                    this.validatorName = false;
                    this.validateName = true;
                }
            },
            'newUser.email': function (value) {
                if(value.length <1 || value.length>25){
                    this.validatorEmail = true;
                    this.validateEmail = false;
                }else{
                    this.validatorEmail = false;
                    this.validateEmail = true;
                }
            },
            'newUser.phone': function (value) {
                this.newUser.phone = value.replace(/[\s|\_|\()]/g,'');
                if(this.newUser.phone.length<13){
                    this.validatorPhone = true;
                    this.validatePhone = false;
                }else{
                    this.validatorPhone = false;
                    this.validatePhone = true;
                }
            },
            completeRegistration: function () {
                if(this.completeRegistration == true){
                    setTimeout(()=>{
                        this.completeRegistration = false;
                    },5000);
                }
            }
        },
        created(){
            // Получаем позиции для формы
           axios({
               url: 'https://frontend-test-assignment-api.abz.agency/api/v1/positions',
               method: 'get'
           }).then(response =>{
               for(let i = 0;i<response.data.positions.length;i++){
                   this.positions.push({position_id:response.data.positions[i].id,position_name:response.data.positions[i].name});
               }
           }).catch(error =>{
               console.log(error);
           });
           // Получаем токен
            axios({
                url: 'https://frontend-test-assignment-api.abz.agency/api/v1/token',
                method: 'get'
            }).then(response =>{
                this.token = response.data.token;
            }).catch(error =>{
                console.log(error);
            });
        },
        mounted(){
            // Валидация формы
            let im = new Inputmask("+38(099) 999 99 99");
            im.mask(document.getElementById('phone'));
            if(window.outerWidth < 899){
                document.querySelector('.subfile').textContent = '';
            }else{
                document.querySelector('.subfile').textContent = 'Upload';
            }
        },
        methods:{
            selectPosition: function(){
                this.activeSelect=!this.activeSelect;
                if(this.newUser.position == null){
                    this.validatorSelect = true;
                }else{
                    this.validatorSelect = false;
                }
            },
            selectedPosition: function (value,position) {
                document.querySelector('.selected-text').textContent = value;
                this.newUser.position = value;
                this.newUser.position_id = position;
                this.activeSelect = false;
                this.validatorSelect = false;
                document.querySelector('.selected-position').classList.add('validate');
            },
            onAttachmentChange: function(e){
                let _URL = window.URL,
                img = new Image(),
                these = this;
                img.onload = function () {
                    if(img.width<70 && img.height<70){
                        these.validatorFile = true;
                        these.validateFile = false;
                        return true;
                    }else{
                        these.validatorFile = false;
                        these.validateFile = true;
                        return  false;
                    }
                };
                img.src = _URL.createObjectURL(e.srcElement.files[0]);
                if(e.srcElement.files[0].size < 5000) {
                    document.querySelector('.file-upload').textContent = '';
                    document.querySelector('.file-upload').textContent = e.target.value;
                    this.newUser.photo = document.getElementById('file').files[0];
                    this.validateFile = true;
                    this.validatorFile = false;
                }else{
                    this.validatorFile = true;
                    this.validateFile = false;
                }
            },
            checkValidate: function(){
                if(document.querySelectorAll('.validate').length === 5){
                    this.activeValidate = false;
                }else{
                    this.activeValidate = true;
                }
            },
            submitRegistration: function(){
                let formData = new FormData();
                formData.append('position_id', this.newUser.position_id);
                formData.append('name', this.newUser.name);
                formData.append('email', this.newUser.email);
                formData.append('phone', this.newUser.phone);
                formData.append('photo', this.newUser.photo);
                if(this.activeValidate == false){
                    axios({
                       url: 'https://frontend-test-assignment-api.abz.agency/api/v1/users',
                       method: 'POST',
                       data: formData,
                       headers: {
                           'Token': this.token,
                           'Content-Type': 'multipart/form-data'
                       }
                    }).then(response =>{
                        this.completeRegistration = true;
                        this.failRegistration = false;
                        location.reload();
                    }).catch(error =>{
                        console.log(error.response.data);
                        this.failRegistration = true;
                        for(let errors in error.response.data.fails){
                        document.querySelector('.fail-request').textContent = error.response.data.fails[errors];
                        }
                    })
                }
            }
        }
    }
</script>
