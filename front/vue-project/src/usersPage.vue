<template>
<header>
<div class="user-header">
    <div class="logo"></div>
    <div class="user-text">
        <p>{{userData.firstName}}</p>
        <p>{{userData.lastName}}</p>
        <p>{{userData.nickName}}</p>
    </div>
</div>
<div class="cont">
    <p>Создать клуб</p>
    <div class="cont-login">
        <input type="text" v-model="title" class="input">
        <input type="text" v-model="description" class="input">
        <button @click="Post()" class="sign">click</button>
    </div>
        <p>clubs</p>
        <div v-for="club in clubs" :key="club" class="clubs">
        <div class="club">
          <img src="./assets/Без имени.png" class="logo-id">
          <div>
            <p>{{club.title}}</p>
            <p>{{club.description}}</p>
            <button @click="Delete(club.id)" class="sign"> Delete</button>
          </div>
        </div>
      </div>
</div>
</header>
</template>
<style>
    .logo{
        width:10vh;
        height:10vh;
        background-color:yellow;
        border-radius:5px;
    }
    .user-header{
        width:100%;
        height:10vh;
        background-color: grey;
        display: flex;
        justify-content: space-around;
    }
    .user-text{
        width:100%;
        color: aliceblue;
        font-size: 1em;
        display: flex;
        justify-content: space-around;
        align-items: center;
    }
</style>
<script setup> 
import axios from 'axios'
import {ref,onMounted} from 'vue'
import { useRouter} from 'vue-router'
let router = useRouter();
let clubs = ref('');
let title = ref('');
let description = ref('')
let result = ref('');
let userData = ref('');

async function getClubs()
{
   await axios.get('https://localhost:7210/clubs')
     .then(function (res) {
       console.log(res);
       return clubs.value = res.data;
})
}
async function Delete(id){
    axios.delete(`https://localhost:7210/clubs/${id}`).then(function(res){
        if(res){
            getClubs();
        }
    })
    console.log(id.value);
    console.log(id);
}
async function getUser(){
    console.log("result "+result)
    await axios.get('https://localhost:7210/api/users/'+ result.value).then(function(responce){
        console.log(responce.data);
        userData.value = responce.data;
        console.log('user '+userData);
        return userData;
    })

}
function Post(){
    axios.post('https://localhost:7210/clubs/create',{
        title:title.value,
        description:description.value
    }).then(function(responce){
        getClubs();
    })   
}

async function checkAuthorize(){
    let acsecc = localStorage.getItem('accessToken');
    let refresh = localStorage.getItem('refreshToken');
    if(acsecc != null && refresh != null){
        console.log(acsecc + '/' + refresh);
        await axios.get('https://localhost:7210/api/auth/check',{ headers: { 'Authorization': "Bearer "+acsecc }}).then(function(res){
            result.value = res.data;
            console.log(result);
        });
    }
    else{
        router.push('/');
    }
}
onMounted(async()=>{
    await getClubs();
    await checkAuthorize();
    await getUser();
})
</script>