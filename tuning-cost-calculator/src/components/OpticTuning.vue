<template>
    <div>
      <h3>Optisches Tuning</h3>
      <b-form-group v-for="option in options" :key="option.id" class="custom-checkbox-group">
        <b-button
          :variant="option.value ? 'success' : 'light'"
          @click="toggleCheckbox(option)"
          class="custom-checkbox-button"
        >
          <i v-if="option.value" class="fas fa-check"></i>
          {{ option.label }}
        </b-button>
      </b-form-group>
    </div>
  </template>
  
  <script>
  import { BButton, BFormGroup } from 'bootstrap-vue';
  
  export default {
    components: {
      BButton,
      BFormGroup,
    },
    props: ['options'],
    methods: {
      toggleCheckbox(option) {
        option.value = !option.value;
      },
    },
  };
  </script>
  
  <style scoped>
  .custom-checkbox-group {
    /* Adjust spacing between checkboxes */
    margin-bottom: 10px;
  }
  
  .custom-checkbox-button {
    display: flex;
    align-items: center;
    width: 160px; /* Adjust the width according to your design */
    padding: 8px; /* Add padding for better touch interaction */
    margin-bottom: 8px; /* Add spacing between buttons */
  }
  
  .custom-checkbox-button i {
    margin-right: 8px; /* Adjust spacing between icon and label */
  }
  
  .custom-checkbox-button:hover {
    cursor: pointer;
  }
  
  .custom-checkbox-button.success:hover {
    background-color: #4caf50; /* Change background color on hover for success variant */
  }
  </style>
  