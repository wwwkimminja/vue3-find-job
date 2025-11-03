<script setup>
import {ref} from 'vue'
import { useRouter } from 'vue-router'
import supabase from '../supabase'

const router= useRouter()
const isLoading= ref(false)

const email=ref('')
const password=ref('')
const handleLogin=async()=>{
  isLoading.value=true

const { data, error } = await supabase.auth.signInWithPassword({
  email: email.value,
  password: password.value,
})
if(error){
  alert(error.message)
}else{
  alert("logged in")
  isLoading.value=false
    router.push('/job-list');
}
}
</script>

<template>
    <div v-if="isLoading" class="loading_info">
    <p>logging in...</p>
  </div>
<div class="form-container">
  <form @submit.prevent="handleLogin">
    <div class="form-group">
      <label for="email" class="email">Email</label>
      <input type="email" id="email" placeholder="enter email" required v-model="email"/>
    </div>
    <div class="form-group">
      <label for="password" class="password">Password</label>
      <input type="password" id="password" placeholder="enter password" required v-model="password"/>
    </div>
    <button type="submit">Login</button>
    <router-link to="/signup">create account</router-link>
  </form>
</div>

</template>

<style scoped lang="scss">
  @use "../style/form.scss"; 
    .loading_info{
    background-color: rgba(0,0,0,0.7);
    position: fixed;
    width: 100vw;
    height: 100vh;
    color: #fff;
    display: grid;
    place-items: center;
  }

</style>
