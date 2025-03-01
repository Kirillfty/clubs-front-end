<template>
    <div class="cont-login">
        <h1 id="login-txt">Логин</h1>
        <input type="text" placeholder="nickname" class="login-input">
        <input type="passowrd" placeholder="password" class="login-input">
        <button class="login-button">Войти</button>
        <h1 @click="GoTo()" id="login-txt-2">Нет аккаунта зарегестрируйтесь</h1>
    </div>
</template>

<script setup>
import { useRouter } from 'vue-router'

let router = useRouter()

function GoTo(){
    
 router.push('/register');
}
</script>