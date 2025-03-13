<template>
    <section class="mb-5">
      <h2 class="text-center mb-4">Why Choose Us?</h2>
      <div class="row">
        <div class="col-lg-4 col-md-6 col-sm-12 mb-4" v-for="(feature, index) in features" :key="index">
          <div class="card h-100">
            <div class="card-body">
              <h5 class="card-title">{{ feature.title }}</h5>
              <p class="card-text">{{ feature.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>
  </template>
  
  <script>
  export default {
    name: 'FeatureSection',
    data() {
      return {
        features: [
          { 
            title: "Diverse Event Selection", 
            description: "Choose from a wide range of events across technology, business, marketing, and finance sectors." 
          },
          { 
            title: "Expert Speakers", 
            description: "Learn from industry leaders and gain valuable insights from experienced professionals." 
          },
          { 
            title: "Networking Opportunities", 
            description: "Connect with like-minded individuals and expand your professional network." 
          },
          { 
            title: "Hands-on Workshops", 
            description: "Participate in practical sessions designed to enhance your skills and knowledge." 
          },
          { 
            title: "Flexible Scheduling", 
            description: "Choose events that fit your calendar with various durations and timings." 
          },
          { 
            title: "Certification", 
            description: "Receive certificates of participation to boost your professional credentials." 
          }
        ]
      };
    }
  };
  </script>