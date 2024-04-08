<template>
  <div class="flex justify-center items-center h-screen">
    <div class="max-w-md w-full p-6 bg-white rounded-lg shadow-lg">
      <h1 class="text-2xl mb-4 font-black">STEP: {{ currentStep.toUpperCase() }}</h1>
      <StepUsername v-if="currentStep === 'username'" :formData="formData" :setUsernameError="setUsernameError" />
      <StepEmail v-else-if="currentStep === 'email'" :formData="formData" :setEmailError="setEmailError" />
      <StepReview v-else :formData="formData" />
      <div class="flex justify-between mt-4">
        
        <button @click="prevStep" :disabled="currentStepIndex === 0" id="btn-prev" :class="{ 'bg-gray-100 text-gray-300': currentStepIndex === 0 }" class="px-4 py-2 text-gray-700 rounded-md focus:outline-none {{ currentStepIndex === 0 ? 'text-white' : 'bg-gray-800' }}">Prev</button>

        <button @click="nextStep" :disabled="isNextDisabled" id="btn-next" :class="{ 'bg-gray-100 text-gray-300': isNextDisabled }" class="px-4 py-2 rounded-md focus:outline-none {{ isNextDisabled ? 'bg-red-400' : 'bg-green-500 text-red-500' }}">Next</button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, reactive, computed } from 'vue';
import StepUsername from './wizard/StepUsername.vue';
import StepEmail from './wizard/StepEmail.vue';
import StepReview from './wizard/StepReview.vue';

export default {
  components: {
    StepUsername,
    StepEmail,
    StepReview
  },
  setup() {
    const steps = ['username', 'email', 'review'];
    const currentStep = ref(steps[0]);
    const formData = reactive({
      username: '',
      email: ''
    });
    const usernameError = ref('');
    const emailError = ref('');

    const currentStepIndex = computed(() => steps.indexOf(currentStep.value));

    const nextStep = () => {
      if (currentStepIndex.value < steps.length - 1) {
        currentStep.value = steps[currentStepIndex.value + 1];
      }
    };

    const prevStep = () => {
      if (currentStepIndex.value > 0) {
        currentStep.value = steps[currentStepIndex.value - 1];
      }
    };

    const setUsernameError = (error) => {
      usernameError.value = error;
    };

    const setEmailError = (error) => {
      emailError.value = error;
    };

    const isNextDisabled = computed(() => {
      // Disable next button if on the last step
      return currentStepIndex.value === steps.length - 1 ||
        (currentStep.value === 'username' && (!formData.username || !!usernameError.value)) ||
        (currentStep.value === 'email' && (!formData.email || !!emailError.value));
    });

    return {
      currentStep,
      formData,
      nextStep,
      prevStep,
      currentStepIndex,
      setUsernameError,
      setEmailError,
      isNextDisabled
    };
  }
};
</script>
