<template>
    <div class="mt-5 mb-9">
      <div class="mb-6"><span class="font-bold text-normal">USERNAME:</span>
        <p>{{formData.username}}</p> </div>
        <div class="mb-3"><span class="font-bold text-normal">E-MAIL:</span>
          <p>{{formData.email}}</p> </div>
    </div>
  </template>
  
  <script>
  export default {
    props: ['formData']
  };
  </script>
  