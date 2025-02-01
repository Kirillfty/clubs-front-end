<template>
    <div class="cont">
        <input type="text" v-model="title">
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
.logo-id{
    width:100px;
    height:100px;
    background-color: yellow;
    border-radius: 50px;
    text-align: center;
}
#id{
    color:black;
    font-size: 25px;
    font-weight: 600;
}
.cont{
    width:100%;
}
.club-cont{
    width:40%;
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
    axios.delete(`https://localhost:7210/clubs/${id}`)
    console.log(id.value);
    console.log(id);
}
function Post(){
    axios.post('https://localhost:7210/clubs',{title:title.value,description:description.value})
}

async function fetchData(){
    axios.get('https://localhost:7210/clubs')
     .then(function (res) {
       console.log(res);
       return clubs.value = res.data;
})
}
 
let intervalId = ref();

onMounted(() => {
      intervalId.value = setInterval(fetchData, 1500); // Запрашиваем данные каждые 5 секунд
});



</script>