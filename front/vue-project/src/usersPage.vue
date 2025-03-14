<template>
<header>
<div class="user-header">
    <div class="logo">
        <img src="./assets/user.png" alt="" class="logo">
    </div>
        <div class="user-text">
            <div id="header-info">
                <p id="info">{{userData.firstName}}</p>
                <p id="info">{{userData.lastName}}</p>
            </div>
            <p id="nick">{{userData.nickName}}</p>
        </div>
</div>
<p align="center">Создай клуб</p>
<div>
        <div class="clubich">
            <input type="text" v-model="title" class="input">
            <br>
            <input type="text" v-model="description" class="input">
            <br>
            <button @click="Post()" class="sign">click</button>
            <br>
        </div>
            
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
.clubich{
    width:40%;
    height:20vh;
    margin:0 auto;
}
#header-info{
    display:flex;
    gap:2%;
}
#info{
    font-size: 2em;
}
    .logo{
        width:20vh;
        height:20vh;
        background-color:yellow;
        border-radius:40%;
    }
    .user-header{
        width:100%;
        padding-top:2%;
        padding-left: 10%;
        display: flex;
        justify-content: space-around;
        align-items: center;
    }
    #nick{
        color:rgb(200, 203, 206);
    }
    .user-text{
        width:100%;
        color: aliceblue;
        font-size: 1em;
        align-items: center;
        margin-left: 5%;
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

function goToClubs(){
    router.push('/clubs');
}
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