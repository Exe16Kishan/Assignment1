<template>
    <section class="mb-5">
      <h2 class="text-center mb-4">Registration Form</h2>
      <form @submit.prevent="submitForm" class="border p-4 rounded">
        <div class="mb-3">
          <label for="username" class="form-label">Username:</label>
          <input type="text" id="username" class="form-control" v-model="registration.username" required>
        </div>
        
        <div class="mb-3">
          <label for="password" class="form-label">Password:</label>
          <input type="password" id="password" class="form-control" v-model="registration.password" required>
        </div>
        
        <div class="mb-3">
          <label for="confirmPassword" class="form-label">Confirm Password:</label>
          <div class="input-group">
            <input type="password" id="confirmPassword" class="form-control" v-model="registration.confirmPassword" required>
            <span class="input-group-text text-danger" v-if="passwordMismatch">Passwords do not match!</span>
          </div>
        </div>
        
        <div class="mb-3">
          <label class="form-label d-block">Select Event Category:</label>
          <div class="form-check form-check-inline" v-for="category in eventCategories" :key="category">
            <input 
              class="form-check-input" 
              type="radio" 
              :id="'reg-'+category" 
              :value="category" 
              v-model="registration.category"
            >
            <label class="form-check-label" :for="'reg-'+category">{{ category }}</label>
          </div>
        </div>
        
        <div class="mb-3">
          <label for="eventSelect" class="form-label">Select Event:</label>
          <select id="eventSelect" class="form-select" v-model="registration.eventName" required>
            <option value="" disabled>Select an event</option>
            <option v-for="event in filteredEventsByCategory" :key="event.eventid" :value="event.eventname">
              {{ event.eventname }}
            </option>
          </select>
        </div>
        
        <button type="submit" class="btn btn-primary">Register</button>
      </form>
  
      <div v-if="registrationSubmitted" class="mt-4 p-3 bg-light rounded">
        <h3>Registration Summary</h3>
        <p><strong>Username:</strong> {{ registration.username }}</p>
        <p><strong>Selected Category:</strong> {{ registration.category }}</p>
        <p><strong>Selected Event:</strong> {{ registration.eventName }}</p>
      </div>
    </section>
  </template>
  
  <script>
  export default {
    name: 'RegistrationForm',
    props: {
      events: {
        type: Array,
        required: true
      }
    },
    data() {
      return {
        registration: {
          username: '',
          password: '',
          confirmPassword: '',
          category: 'Business',  // Default value
          eventName: ''
        },
        registrationSubmitted: false
      };
    },
    computed: {
      eventCategories() {
        return [...new Set(this.events.map(event => event.category))];
      },
      filteredEventsByCategory() {
        return this.events.filter(event => event.category === this.registration.category);
      },
      passwordMismatch() {
        return this.registration.password !== this.registration.confirmPassword && 
               this.registration.confirmPassword !== '';
      }
    },
    methods: {
      submitForm() {
        if (this.passwordMismatch) {
          alert("Passwords do not match!");
          return;
        }
        
        this.registrationSubmitted = true;
      }
    }
  };
  </script>
  
  <style scoped>
  .form-check-inline {
    margin-right: 1rem;
  }
  </style>