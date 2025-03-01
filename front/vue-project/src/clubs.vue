<template>
    
    
</template>
<style scoped>


</style>
<script setup>
import {ref} from 'vue'
import axios from 'axios'
let clubs = ref([])

async function fetchData(){
    axios.get('https://localhost:7210/clubs')
     .then(function (res) {
       console.log(res);
       return clubs.value = res.data;
})
}
 






</script>