<template>
    <div>
      <input type="text" id="email" name="email" class="mt-6 mb-6 w-full rounded-lg" v-model="formData.email" @input="validateEmail"/>
      <div v-if="emailError" class="text-sm italic text-red-500">{{ emailError }}</div>
    </div>
    
  </template>
  
  <script>
  export default {
    props: ['formData', 'setEmailError'],
    data() {
      return {
        emailError: ''
      };
    },
    methods: {
      validateEmail() {
        // Validation logic for email
        if (!this.formData.email) {
          this.emailError = 'Email is required.';
        } else if (!/\S+@\S+\.\S+/.test(this.formData.email)) {
          this.emailError = 'Invalid email address.';
        } else {
          this.emailError = '';
        }
        // Pass the error state to the parent component
        this.setEmailError(this.emailError);
      }
    }
  };
  </script>
  