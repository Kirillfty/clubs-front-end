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
<style scoped>
input{
    width:20%;
    padding:1%;
    border-radius:10px;
    border-color:purple;
    background: none;
    margin-top:1%;
}
button{
    width:15%;
    padding:1%;
    border-color:purple;
    background: none;
    margin-top:1%;
    border-radius:10px;

}
.logo-id{
    width:100px;
    height:100px;
    background-color: yellow;
    border-radius: 10px;
    text-align: center;
}
#id{
    color:black;
    font-size: 25px;
    font-weight: 600;
}
.cont{
    
    margin-top:10%;
    gap:5%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    
}
.club-cont{
    width:100%;
    border:1px solid grey;
    padding:2%;
    display: flex;
    border-radius: 15px;
    justify-content: space-between;
    margin-top: 5%;
}

</style>
<script setup>
import {ref,onMounted} from 'vue'
import axios from 'axios'
let clubs = ref([])
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

async function fetchData(){
    axios.get('https://localhost:7210/clubs')
     .then(function (res) {
       console.log(res);
       return clubs.value = res.data;
})
}
 






</script>