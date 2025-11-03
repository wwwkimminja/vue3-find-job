<script setup>
import supabase from '../supabase';
import { onMounted } from 'vue';
import { useRouter } from 'vue-router';
import { ref } from 'vue';

const router=useRouter()
const isLogin = ref(false)
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
    <h1>User Profile</h1>

  </div>

</template>

<style scoped lang="scss">


</style>
