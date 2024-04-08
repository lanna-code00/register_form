<template>
    <div>
      <!-- <label for="username" >Username:</label> -->
      <input type="text" id="username" name="username" class="mt-6 mb-6 w-full rounded-lg" v-model="formData.username" @input="validateUsername" />
      <div v-if="usernameError" class="text-sm italic text-red-500">{{ usernameError }}</div>
    </div>
  </template>
  
  <script>
  export default {
    props: ['formData', 'setUsernameError'],
    data() {
      return {
        usernameError: ''
      };
    },
    methods: {
      validateUsername() {
        // Validation logic for username
        if (!this.formData.username) {
          this.usernameError = 'Username is required.';
        } else if (this.formData.username.length < 3 || this.formData.username.length > 20) {
          this.usernameError = 'Username must be between 3 and 20 characters.';
        } else if (!/^[a-zA-Z0-9_]+$/.test(this.formData.username)) {
          this.usernameError = 'Invalid Username, it can only contain letters, numbers, and underscores.';
        } else {
          this.usernameError = '';
        }
        // Pass the error state to the parent component
        this.setUsernameError(this.usernameError);
      }
    }
  };
  </script>
  