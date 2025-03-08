<template>
    <div class="cont">
        <input type="text" v-model="title" >
        <input type="text" v-model="description">
        <button @click="Post()">click</button>
        <p>clubs</p>
        <div v-for="club in clubs" :key="club" class="clubs">
            <div class="club-cont" >
                <button @click="Delete(club.id)">delete</button>
                <div class="logo-id">
                    <p id="id">{{club.id}}</p>
                </div>
                <p>{{club.title}}</p>
                <p>{{club.description}}</p>
            </div>
        </div>
</div>
</template>
<script setup> 
import axios from 'axios'
function Page(){
    let acsecc = localStorage.getItem('accessToken');
    let refresh = localStorage.getItem('refreshToken');
    if(acsecc != null && refresh != null){
        
    }
    else{
        routerKey.push('/');
    }
}
</script>