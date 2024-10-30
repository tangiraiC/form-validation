<script setup>
import { ref, computed } from "vue";
const formData  =ref([{
    name:"",
    email:"",
    password:"",
}])
 const isNamevalid  = computed(() => formData.value[0].name.trim() !=="");
 const isEmailvalid = computed(() =>  /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(formData.value[0].email));
 const isPasswordvalid = computed(() => formData.value[0].password.length  >= 8 );
 const isFormvalid = computed(() => isNamevalid.value && isEmailvalid.value && isPasswordvalid.value)

 const submitForm = () => {
  if (isFormvalid.value) {
    // a lot of logic
    console.log('form submitted  ', formData.value)

  }else{
    console.log('form is invalid. please check its field')
  }
 }
</script>
<template>

  <div>
    <form @submit.prevent="submitForm" class="custom-form">
      <div class="form-group">
        <label for="name">Name  :</label>
        <input type="text" id="name" v-model="formData.name">
        <span v-if="!isNamevalid" class="error" > name is required</span>

      </div>
      <div class="form-group">
        <label for="email">Email  :</label>
        <input type="email" id="email" v-model="formData.email">
        <span v-if="!isEmailvalid" class="error" > email is required</span>

      </div>
      <div class="form-group">
        <label for="password">Password  :</label>
        <input type="password" id="password" v-model="formData.password">
        <span v-if="!isPasswordvalid" class="error" > password must be atleast 8 characters</span>

      </div>
      <button type="submit" :disabled="!isFormvalid" class="submit-button">submit</button>

    </form>
  </div>
</template>
<style scoped>
.custom-form {
  max-width: 400px;
  margin: 0 auto;
}

.form-group {
  margin-bottom: 20px;
}

label {
  display: block;
  font-weight: bold;
  margin-bottom: 5px;
}

input {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.error {
  color: #e74c3c;
  font-size: 14px;
  margin-top: 5px;
}

.submit-button {
  padding: 10px 15px;
  font-size: 16px;
  background-color: #3498db;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.submit-button:disabled {
  background-color: #bdc3c7;
  cursor: not-allowed;
}
</style>
