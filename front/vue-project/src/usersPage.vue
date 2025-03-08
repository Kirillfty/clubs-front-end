<template>
    <div class="cont">
        <input type="text" v-model="title" >
        <input type="text" v-model="description">
        <button @click="Post()">click</button>
        <p>clubs</p>
        <div v-for="club in clubs" :key="club" class="clubs">
        <div class="club">
          <img src="./assets/Без имени.png" class="logo-id">
          <div>
            <p>{{club.title}}</p>
            <p>{{club.description}}</p>
          </div>
        </div>
      </div>
</div>
</template>
<script setup> 
import axios from 'axios'
import {ref,onMounted} from 'vue'
let clubs = ref('');
async function fetchData()
{

   await axios.get('https://localhost:7210/clubs')
     .then(function (res) {
       console.log(res);
       return clubs.value = res.data;
})

}
let title = ref('');
let description = ref('')
let result = ref('');
function Post(){
    axios.post('https://localhost:7210/clubs/create',{
        title:title.value,
        description:description.value
    })

}
async function Page(){
    let acsecc = localStorage.getItem('accessToken');
    let refresh = localStorage.getItem('refreshToken');
    if(acsecc != null && refresh != null){
        console.log(acsecc + '/' + refresh);
        axios.get('https://localhost:7210/api/auth/check',{ headers: { 'Authorization': "Bearer "+acsecc }}).then(function(res){
            result = res.data;
            console.log(result);
        });
    }
    else{
        routerKey.push('/');
    }
}
onMounted(async()=>{
    await fetchData();
    await Page();
})
</script>