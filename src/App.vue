<template>
  <div id="app">
    <nav>
      <button @click="section = 'home'">Home</button>
      <button @click="section = 'projects'">Projects</button>
      <button @click="section = 'contact'">Contact</button>
    </nav>

    <div v-if="section === 'home'">
      <h1>Carson's Website</h1>
      <p v-if="showWelcome">Welcom to my website! Click the button to show that you visited!</p>
      <button @click="showWelcome = !showWelcome">
        {{ showWelcome ? 'Hide Welcome Message' : 'Show Welcome Message' }}
      </button>
    </div>

    <div v-if="section === 'projects'">
      <h2>My Projects</h2>
      <p v-if="projects.length === 0">No projects available</p>
      <ul v-else>
        <li v-for="project in projects" :key="project.id">{{ project.name }}</li>
      </ul>
      <p>Total Projects: {{ projectCount }}</p>
    </div>

    <div v-if="section === 'contact'">
      <h2>Contact Me</h2>
      <form @submit.prevent="submitForm">
        <label>Name:</label>
        <input v-model="contactForm.name" @input="logInput('name')" required />

        <label>Email:</label>
        <input v-model="contactForm.email" @input="logInput('email')" required />

        <label>Message:</label>
        <textarea v-model="contactForm.message" @input="logInput('message')"></textarea>

        <button type="submit">Submit</button>
      </form>
    </div>

    <div>
      <h3>Visitor Counter: {{ counter }}</h3>
      <button @click="counter++">Click Me!</button>
    </div>
  </div>
</template>

<script>
import { ref, computed, watch } from 'vue';

export default {
  setup() {
    const section = ref('home');
    const showWelcome = ref(true);
    const projects = ref([
      { id: 1, name: 'Color Selector App' },
      { id: 2, name: 'Personal Website (html)' },
      { id: 2, name: 'This Website!' }
    ]);

    const projectCount = computed(() => projects.value.length);

    const contactForm = ref({
      name: '',
      email: '',
      message: ''
    });

    const logInput = (field) => {
      console.log(`${field} changed:`, contactForm.value[field]);
    };
    
    const counter = ref(0);

    const submitForm = () => {
      alert('Form submitted successfully!');
    };

    return {
      section,
      showWelcome,
      projects,
      projectCount,
      contactForm,
      logInput,
      submitForm,
      counter
    };
  }
};
</script>



