<script setup>
import {ref} from 'vue'

const email=ref('')
const password=ref('')
const handleLogin=()=>{
  console.log(email.value,password.value)
}
</script>

<template>
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

</style>
