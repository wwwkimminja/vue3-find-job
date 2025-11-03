<script setup>
import {Icon} from '@iconify/vue'
import {useRoute} from 'vue-router'
import { ref, watch } from 'vue'   

let route = useRoute();
let currentPath = route.path;
let title = ref('')



watch(route,(newPath)=>{
  currentPath = newPath.path

    if(currentPath === '/') {
      title.value = 'Log in'; 
    } else if (currentPath === '/signup') {
      title.value = 'Sign up';
    } else if (currentPath === '/job-list') {
      title.value = 'Job List';
    } else if (currentPath === '/job-detail') {
      title.value = 'Job Detail';
    } else if (currentPath === '/job-post') {
      title.value = 'Job Post'
    } else if (currentPath === '/user-profile') {
      title.value = 'Profile'
    }

})

</script>

<template>
<nav>
  <h1>{{ title }}</h1>

  <router-link v-if="currentPath === '/' 
          || currentPath === '/signup' 
          || currentPath === '/job-post'"
      to="/job-list" 
      class="btn-close">
  <Icon 
  style ="color: var(--text-color-dark);"
  icon="material-symbols:close" width="24" height="24" />
  </router-link>
  <router-link 
      v-if="currentPath === '/job-detail' || currentPath === '/user-profile'"
      to="/job-list" 
      class="btn-close">
      <Icon 
        icon="ic:baseline-arrow-back" 
        width="24" 
        height="24"  
        style="color: 1e1e1e" 
      />
  </router-link>
    
  <router-link 
	      v-if="currentPath === '/job-detail' || currentPath === '/user-profile'"
	      to="/job-list" 
	      class="btn-close"
	    >
	      <Icon 
	        icon="ic:baseline-arrow-back" 
	        width="24" 
	        height="24"  
	        style="color: 1e1e1e" 
	      />
	    </router-link>
      <div class="right-icons" v-if="currentPath === '/job-list'">
      <router-link to="/user-profile">
        <Icon 
          icon="teenyicons:user-circle-solid" 
          width="24"
          style="color: #1e1e1e;"
        />
      </router-link>
      <router-link to="/job-post">
        <Icon 
        icon="mdi:pencil-outline"  
          width="24"
          style="color: #1e1e1e;"
        />
      </router-link>
  </div>


</nav>
</template>

<style lang="scss" scoped>
  nav {
    position: relative;
    border-bottom: 1px solid #ccc;
    width: 100%;
    height: 44px;
    padding: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    h1 {
      font-size: 16px;
      color: var(--text-color-dark);
    }
    .btn-close {
      position: absolute;
      left: 15px;
      text-decoration: none;
    }
    .right-icons{
      position:absolute;
      right: 15px;
      top:10px;
      display: flex;
      gap:10px;
    }
  }  
  </style>
