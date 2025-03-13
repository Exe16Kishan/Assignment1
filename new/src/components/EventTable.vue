<template>
    <section class="mb-5">
      <h2 class="text-center mb-4">Event Information</h2>
      
      <div class="row mb-4">
        <div class="col-md-4 mb-3">
          <label for="eventIdSearch" class="form-label">Search by Event ID:</label>
          <input 
            type="text" 
            id="eventIdSearch" 
            class="form-control" 
            v-model="filters.eventId"
            placeholder="Enter event ID"
          >
        </div>
        <div class="col-md-4 mb-3">
          <label for="eventNameSearch" class="form-label">Search by Event Name:</label>
          <input 
            type="text" 
            id="eventNameSearch" 
            class="form-control" 
            v-model="filters.eventName"
            placeholder="Enter event name"
          >
        </div>
        <div class="col-md-4 mb-3">
          <label for="durationSearch" class="form-label">Search by Duration:</label>
          <input 
            type="text" 
            id="durationSearch" 
            class="form-control" 
            v-model="filters.duration"
            placeholder="Enter duration in hours"
          >
        </div>
      </div>
  
      <div class="row mb-4">
        <div class="col-12">
          <label class="form-label d-block">Filter by Category:</label>
          <div class="form-check form-check-inline" v-for="category in categories" :key="category">
            <input 
              class="form-check-input" 
              type="radio" 
              :id="category" 
              :value="category" 
              v-model="filters.category"
              :checked="filters.category === category"
            >
            <label class="form-check-label" :for="category">{{ category }}</label>
          </div>
        </div>
      </div>
  
      <div class="table-responsive">
        <table class="table table-striped table-hover">
          <thead>
            <tr>
              <th>Event ID</th>
              <th>Event Name</th>
              <th>Category</th>
              <th>Duration (Hours)</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="event in filteredEvents" :key="event.eventid">
              <td>{{ event.eventid }}</td>
              <td>{{ event.eventname }}</td>
              <td>{{ event.category }}</td>
              <td>{{ event.durationhour }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </section>
  </template>
  
  <script>
  export default {
    name: 'EventTable',
    props: {
      events: {
        type: Array,
        required: true
      }
    },
    data() {
      return {
        filters: {
          eventId: '',
          eventName: '',
          duration: '',
          category: 'All'
        }
      };
    },
    computed: {
      categories() {
        const uniqueCategories = [...new Set(this.events.map(event => event.category))];
        return ['All', ...uniqueCategories];
      },
      filteredEvents() {
        return this.events.filter(event => {
          const matchesEventId = event.eventid.toLowerCase().includes(this.filters.eventId.toLowerCase());
          const matchesEventName = event.eventname.toLowerCase().includes(this.filters.eventName.toLowerCase());
          const matchesDuration = this.filters.duration === '' || event.durationhour.toString() === this.filters.duration;
          const matchesCategory = this.filters.category === 'All' || event.category === this.filters.category;
          
          return matchesEventId && matchesEventName && matchesDuration && matchesCategory;
        });
      }
    }
  };
  </script>
  
  <style scoped>
  .form-check-inline {
    margin-right: 1rem;
  }
  </style>