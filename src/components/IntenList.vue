<script setup>
import { ref } from 'vue';
import axios from 'axios';

const intern = ref({
  name: '',
  phone: '',
  email: '',
  university: '',
  startDate: '',
});

const welcomeEmail = ref(false);

const submitForm = async () => {
  try {

    const internData = { ...intern.value,welcomeEmail: welcomeEmail.value };

    const response = await axios.post('https://intern-test-app-be-production.up.railway.app/api/intern/submit', internData);
    alert(response.data);
  } catch (error) {
    console.error('Error submitting form:', error);
    alert('Error submitting form.');
  }
};
</script>

<template>
  <div class="container mx-auto p-4">
    <h1 class="text-2xl mb-4">Intern Registration</h1>
    <form @submit.prevent="submitForm" class="space-y-4">
      <div>
        <label for="name" class="block">Full Name</label>
        <input v-model="intern.name" type="text" id="name" class="border p-2 w-full" />
      </div>
      <div>
        <label for="phone" class="block">Phone</label>
        <input v-model="intern.phone" type="text" id="phone" class="border p-2 w-full" />
      </div>
      <div>
        <label for="email" class="block">Email</label>
        <input v-model="intern.email" type="email" id="email" class="border p-2 w-full" />
      </div>
      <div>
        <label for="email" class="block">University</label>
        <input v-model="intern.university" type="text" id="university" class="border p-2 w-full" />
      </div>
      <div>
        <label for="startDate" class="block">Start Date</label>
        <input v-model="intern.startDate" type="date" id="startDate" class="border p-2 w-full" />
      </div>
      <div>
        <input v-model="welcomeEmail" type="checkbox" id="scheduleEmail" class="mr-2" />
        <label for="scheduleEmail">Schedule Welcome Email (5 days in advance)</label>
      </div>
      <button type="submit" class="bg-blue-500 text-white p-2 mt-4">Submit</button>
    </form>
  </div>
</template>

<style scoped></style>
