<template>
     <div class="cont">
        <h1>register</h1>
        <input type="text" placeholder="name" v-model="Acc.firstName">
        <input type="text" placeholder="lastname" v-model="Acc.lastName">
        <input type="text" placeholder="nickname" v-model="Acc.nickName">
        <input type="passowrd" placeholder="password" v-model="Acc.password">
        <button @click="GoTo()">register</button>
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
axios.post('https://localhost:7210/api/users',{firstName:Acc.value.firstName,
lastName:Acc.value.lastName,
nickName:Acc.value.nickName,
password:Acc.value.password,

}).then(function(responce){
    if(responce){
        router.push('/');
    }
    else{
        console.log('non correct values');
    }
});
}
</script>