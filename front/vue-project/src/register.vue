<template>
     <div class="cont-reg">
        <h1 id="login-txt">Регистрация</h1>
        <input type="text" placeholder="name" v-model="Acc.firstName" class="login-input">
        <input type="text" placeholder="lastname" v-model="Acc.lastName" class="login-input">
        <input type="text" placeholder="nickname" v-model="Acc.nickName" class="login-input">
        <input type="passowrd" placeholder="password" v-model="Acc.password" class="login-input">
        <button @click="Registration()" class="login-button">Регистрация</button>
        <h1  @click="() => {router.push('/')}"  id="login-txt-2">Усть аккаунт.Войди</h1>
    </div>
</template>

<script setup>
import {ref} from 'vue'
import { useRouter} from 'vue-router'
import axios from 'axios'
let Acc = ref({
    firstName:'',
    lastName:'',
    nickName:'',
    password:''
})
let router = useRouter();
function Registration(){
axios.post('https://localhost:7210/api/users',{firstName:Acc.value.firstName,
lastName:Acc.value.lastName,
nickName:Acc.value.nickName,
password:Acc.value.password,

}).then(function(responce){
    if(responce){
        router.push('/clubs');
    }
    else{
        console.log('non correct values');
    }
});
}
</script>