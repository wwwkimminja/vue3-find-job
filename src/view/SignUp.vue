<script setup>
import {ref} from 'vue'

const email=ref('')
const password=ref('')
const tel=ref('')
const text=ref('')
const handleSignup=()=>{
  console.log(email.value,password.value,tel.value,text.value)
}
</script>

<template>
<div class="form-container">
  <form @submit.prevent="handleSignup">
    <div class="form-group">
      <label for="email" class="email">Email</label>
      <input type="email" id="email" placeholder="enter email" required v-model="email"/>
    </div>
    <div class="form-group">
      <label for="password" class="password">Password</label>
      <input type="password" id="password" placeholder="enter password" required v-model="password"/>
    </div>
    <div class="form-group">
      <label for="tel" class="tel">Tel</label>
      <input type="tel" id="tel" placeholder="080-123-1234" required v-model="tel"/>
    </div>
    <div class="form-group">
      <label for="text" >Career</label>
      <textarea type="text" id="text"  required v-model="text"/>
    </div>
    <button type="submit">Sign up</button>
 
  </form>
</div>
</template>



<style lang="scss">

  @use "../style/form.scss"; 

</style>
