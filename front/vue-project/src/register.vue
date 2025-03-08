<template>
     <div class="cont-reg">
        <!-- From Uiverse.io by Yaya12085 --> 
<div class="form-container">
	<input type="text" v-model="Acc.firstName" placeholder="fistaname">
	<input type="text" v-model="Acc.lastName" placeholder="lastname">
	<input type="text" v-model="Acc.nickName"placeholder="nickname">
	<input type="text" v-model="Acc.password" placeholder="password">
	<button @click="Registration()" class="sign">click</button>
</div> 
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
function GoTo(){
    router.push('/');
}
async function Registration(){
await axios.post('https://localhost:7210/api/auth/register',{firstName:Acc.value.firstName,
lastName:Acc.value.lastName,
nickName:Acc.value.nickName,
password:Acc.value.password,

}).then(function(responce){
    if(responce){
        router.push('/clubs');
        localStorage.clear();
        localStorage.setItem('accessToken',responce.data.accessToken);
        localStorage.setItem('refreshToken',responce.data.refreshToken);
    }
    else{
        console.log('non correct values');
    }
});
}
</script>