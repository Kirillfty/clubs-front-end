<template>
    <div class="cont">
        <h1>login</h1>
        <input type="text" placeholder="nickname"><br><br>
        <input type="passowrd" placeholder="password"><br><br>
        <button @click="GoTo()">register</button>
    </div>
</template>

<script setup>
import { useRouter } from 'vue-router'
let router = useRouter()

function GoTo(){
 router.push('/clubs');
}
</script>