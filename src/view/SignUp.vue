<script setup>
import {ref} from 'vue'
import supabase from '../supabase'
import {useRouter} from 'vue-router'
const router = useRouter()

const email=ref('')
const password=ref('')
const tel=ref('')
const text=ref('')
const name=ref('')
const address = ref('')
const isLoading = ref(false)



const handleSignup=async()=>{
  isLoading.value = true
  const { data, error } = await supabase.auth.signUp({
  email: email.value,
  password: password.value,
})

if(error){
  alert(error.message)
}else{
  const { error } = await supabase
  .from('user_table')
  .insert({ tel:tel.value,text:text.value, name:name.value,address:address.value })

  if(error){
    alert(error.message)
  }else{
     alert("successfully sign up")
      isLoading.value = false
      router.push('/')
  }
}
}
</script>

<template>
  <div v-if="isLoading" class="loading_info">
    <p>signing up...</p>
  </div>
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
      <label for="name" >Name</label>
      <input type="text" id="name" placeholder="enter name"required v-model="name"/>
    </div>
    <div class="form-group">
      <label for="address" >Address</label>
      <input type="text" id="address" placeholder="enter address" required v-model="address"/>
    </div>
        <div class="form-group">
      <label for="text" >Introduce</label>
      <textarea type="text" id="text"  required v-model="text"/>
    </div>
    <button type="submit">Sign up</button>
 
  </form>
</div>
</template>



<style lang="scss">

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
