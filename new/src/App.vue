<template>
  <div class="container mt-4">
    <HeaderSection />
    <FeatureSection />
    <EventTable :events="events" />
    <RegistrationForm :events="events" />
  </div>
</template>

<script>
import HeaderSection from './components/HeaderSection.vue';
import FeatureSection from './components/FeatureSection.vue';
import EventTable from './components/EventTable.vue';
import RegistrationForm from './components/RegistrationForm.vue';
import { events } from './assets/events.js';

export default {
  name: 'App',
  components: {
    HeaderSection,
    FeatureSection,
    EventTable,
    RegistrationForm
  },
  data() {
    return {
      events
    };
  }
};
</script>