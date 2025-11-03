<script setup>
import supabase from '../supabase';
import { onMounted } from 'vue';
import { useRouter } from 'vue-router';
import { ref } from 'vue';

const router=useRouter()
const isLogin = ref(false)

const handleLogout=async()=>{
  const { error } = await supabase.auth.signOut()
  if(error){
alert('Failed log out')
  }else{
alert('logged out')
router.push('/')
  }
}
onMounted(async()=>{
const { data: { user } } = await supabase.auth.getUser()
  console.log(user?.email)

  if(user){
 console.log('logged in')
 isLogin.value=true
  }else{
    alert('Available after logging in')
    router.push('/')
  }

})
</script>

<template>
  <div class="container" v-if="isLogin">
   <div class="form-container">
    <button class="logout" @click="handleLogout">Log out</button>
   </div>

  </div>

</template>

<style scoped lang="scss">
  button { 
    background: transparent;
    color: var(--main-color);
    font-size: 16px;
    margin-top: 40px;
    &:hover{
      opacity: 0.7;
      text-decoration: underline;
    }
  }


</style>
