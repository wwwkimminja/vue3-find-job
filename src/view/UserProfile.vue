<script setup>
import supabase from '../supabase';
import { onMounted } from 'vue';
import { useRouter } from 'vue-router';
import { ref } from 'vue';

const router=useRouter()
const isLogin = ref(false)
const name = ref('name')
const addr=ref('addr')
const test=ref('intro')

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
 const { data, error } = await supabase
  .from('user_table')
  .select().eq('id',user.id)

  if(data){
    console.log('user data:',data);
    name.value = data[0].name;
    addr.value = data[0].address;
    test.value = data[0].text;
  }
  }else{
    alert('Available after logging in')
    router.push('/')
  }

})
</script>

<template>
  <div class="container" v-if="isLogin">
    <div class="top-info-box">
      <img src="/vite.svg" alt="">
      <div class="right-info">
        <span class="name">{{name}}</span>
        <address>{{addr}}</address>
      </div>
    </div>
    <div class="text-info">
      <h4>introduction</h4>
      <p>{{ intro }}</p>
    </div>
    <button class="logout" @click="handleLogout">Log out</button>

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

    .form-container {
    margin-top: 20px;
  }
  .top-info-box {
    display: flex;
    align-items: center;
    margin-bottom: 40px;

    img {
      width: 40px;
      height: 40px;
      border-radius: 50%;
      margin-right: 12px;
    }

    .right-info {
      width: 100%;
      line-height: 1.4;
  
      .name {
        font-size: 16px;
        font-weight: 600;
      }
      address {
        font-size: 14px;
        font-weight: 400;
        font-style: normal;
        color: #777;
      }
    }
  }
    .text-info {
    margin-bottom: 25px;
    h4 {
      margin-bottom: 8px;
    }
    p {
      font-size: 14px;
      color: #333;
      line-height: 20px;
      border: 1px solid #d9d9d9;
      border-radius: 8px;
      padding: 12px 1rem;
    }
  }




</style>
