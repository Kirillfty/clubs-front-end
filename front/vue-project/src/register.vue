<template>
     <div class="cont">
        <h1>register</h1>
        <button @click="GoTo()">click</button>
        <input type="text" placeholder="name">
        <input type="text" placeholder="lastname">
        <input type="text" placeholder="nickname">
        <input type="passowrd" placeholder="password">
        <button>register</button>
    </div>
</template>

<script setup>
import { useRouter } from 'vue-router'
let router = useRouter();
function GoTo(){
 router.push('/');
}
</script>