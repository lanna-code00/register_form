<template>
  <div>
    <input v-model="description" type="text" id="description" name="description" />
    <p v-if="checkBalanced(description)" data-testid="balanced-message">{{ balancedMessage }}</p>
    <p v-else data-testid="unbalanced-message">{{ unbalancedMessage }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const balancedMessage = 'The text is balanced.';
const unbalancedMessage = 'The text is not balanced.';
const description = ref('');

const checkBalanced = (text) => {
  text = String(text); // Ensure text is a string
  const stack = [];
  const brackets = { '(': ')', '[': ']', '{': '}' };
  
  for (let char of text) {
    if (brackets.hasOwnProperty(char)) {
      stack.push(char);
    } else if (Object.values(brackets).includes(char)) {
      if (stack.length === 0 || brackets[stack.pop()] !== char) {
        return false;
      }
    }
  }
  
  return stack.length === 0;
};

// Expose checkBalanced for testing
defineExpose({ checkBalanced });
</script>
