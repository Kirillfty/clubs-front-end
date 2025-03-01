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
let title = ref('')
let description = ref('')
async function Delete(id){
    axios.delete(`https://localhost:7210/clubs/${id}`).then(function(res){
        if(res){
            fetchData();
        }
    })
    console.log(id.value);
    console.log(id);
}
function Post(){
    axios.post('https://localhost:7210/clubs/create',{title:title.value,description:description.value})
    .then(function(res){
        if(res){
            fetchData();
        }
    })
}
</script>