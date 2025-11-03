<script setup>

import { ref } from 'vue';
  import { Icon } from '@iconify/vue';

  const title = ref('');
  const todo = ref('');
  const pay_rule = ref('');
  const pay = ref('');
  const desc = ref('');
  const company_name = ref('');
  const location = ref('');
  const tel = ref('');


</script>

<template>
<div class="form-container">
  <form>
     <!-- 1.title -->
    <div class="form-group">
        <label for="title">title</label>
        <input 
          type="text" 
          id="title" 
          required
          placeholder="summarize the job"
          v-model="title"
        >
    </div>

          <!-- 2.task -->
      <div class="form-group">
        <label for="todo">task</label>
        <input 
          type="text" 
          id="todo" 
          v-model="todo"
          placeholder="enter the tasks to be done."
          required
        />
      </div>

            <!-- 3.select hourly monthly -->
      <div class="form-group">
        <input type="radio" id="pay_rule1" name="pay_rule" value="hourly" v-model="pay_rule" required checked>
        <input type="radio" id="pay_rule2" name="pay_rule" value="monthly" v-model="pay_rule" required >
        <div class="tab-group">
          <label for="pay_rule1">hourly pay</label>
          <label for="pay_rule2">monthly pay</label>
        </div>
        <!-- 4.pay-->
        <input 
          type="number" 
          id="pay" 
          placeholder="enter your hourly or monthly pay."
          v-model="pay" 
          required
        >
      </div>

            <!-- 5.description -->
      <div class="form-group">
        <label for="desc">description</label>
        <textarea 
          name="desc" 
          id="desc" 
          v-model="desc"
          rows="4"
          required
          placeholder="the specific job description, working conditions, and the skills required of the applicant, as well as any other preferential factors."
        ></textarea>
      </div>

            <!-- 6.company name-->
      <div class="form-group">
        <label for="company_name">company name</label>
        <input 
          type="text" 
          id="company_name" 
          v-model="company_name" 
          required
          placeholder="ABC company"
        >
      </div>

      <!-- 7.location -->
      <div class="form-group">
        <label for="location">location</label>
        <input 
          type="text" 
          id="location" 
          v-model="location" 
          required 
          placeholder="shinjuku tokyo"
        >
      </div>

            <!-- 8.tel -->
      <div class="form-group">
        <label for="tel">tel</label>
        <input type="text" id="tel" v-model="tel" required placeholder="080-1234-5678">
      </div>


      <!-- 9.photo-->
      <div class="form-group">
        <label for="photo">
          <p class="title">photo</p>
          <figure>
            <Icon icon="mdi-light:camera" width="64" height="64"  style="color: #1e1e1e;" />
            <img src="/box64.jpg" alt="미리보기" width="64" height="64" />
          </figure>
        </label>
        <input type="file" id="photo" accept="image/*">
      </div>

  </form>
</div>
</template>

<style scoped lang="scss">

  @use "../style/form.scss";

  .form-container {
    margin-top: 20px;
    padding-bottom: 50px;

    .tab-group {
      display: flex;
      gap: 15px;
      label { 
        flex: 1;
        border: 1px solid var(--main-color-dark);
        border-radius: 8px;
        text-align: center;
        padding: 12px;
      }
    }

    input[type="radio"] {
        display: none;
    }

    input[type="radio"]:nth-child(1):checked ~ .tab-group label:nth-child(1) {
      background: var(--main-color-dark);
      color: #fff;
    }

    input[type="radio"]:nth-child(2):checked ~ .tab-group label:nth-child(2) {
      background: var(--main-color-dark);
      color: #fff;
    }
   #pay { margin-top: 8px;}

  
    .form-group:has(label[for=photo]) input {
      border: none;
    }


    label[for=photo] {
      figure { 
        display: flex; 
        align-items: center;
        img { 
          border: 1px solid red;
          margin-left: 30px; 
        }
      }
    }
    input[type="file"] {
      display: none;
    }
  }

  .btn-submit {
    background: var(--main-color-light);
  }

  .form-group:has(label[for=photo]) {
    padding-bottom: 25px;
    border-bottom: 5px solid #ccc;
  }

</style>
