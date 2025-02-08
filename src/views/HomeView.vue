<template>
  <div class="container">
    <h1 class="title">Survey Form</h1>
    <form @submit.prevent="submitForm">
      <div class="form-group" v-for="(question, index) in questions" :key="index">
        <label>{{ question.label }}</label>
        <template v-if="question.type === 'text'">
          <input type="text" v-model="answers[index]" />
        </template>
        <template v-else-if="question.type === 'radio'">
          <div v-for="option in question.options" :key="option">
            <input type="radio" :value="option" v-model="answers[index]" /> {{ option }}
          </div>
        </template>
        <template v-else-if="question.type === 'checkbox'">
          <div v-for="option in question.options" :key="option">
            <input type="checkbox" :value="option" v-model="answers[index]" /> {{ option }}
          </div>
        </template>
      </div>
      <button type="submit">Submit</button>
    </form>
    <div v-if="submitted">
      <h2>Survey Results:</h2>
      <pre>{{ answers }}</pre>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const questions = ref([
  { label: "What is your name?", type: "text" },
  { label: "What is your favorite color?", type: "radio", options: ["Red", "Blue", "Green"] },
  { label: "Which programming languages do you know?", type: "checkbox", options: ["JavaScript", "Python", "C++"] },
  { label: "What is your age?", type: "text" },
  { label: "What is your preferred development environment?", type: "radio", options: ["Windows", "Mac", "Linux"] },
  { label: "Which databases have you worked with?", type: "checkbox", options: ["MySQL", "PostgreSQL", "MongoDB", "SQLite"] },
  { label: "How many years of experience do you have in programming?", type: "text" }
]);

const answers = ref({});
const submitted = ref(false);

onMounted(() => {
  questions.value.forEach((question, index) => {
    if (question.type === 'checkbox') {
      answers.value[index] = [];
    }
  });
});

const submitForm = () => {
  submitted.value = true;
  console.log("Survey submitted:", answers.value);
};
</script>

<style>
.container {
  max-width: 500px;
  margin: auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
.title {
  text-align: center;
}
.form-group {
  margin-bottom: 15px;
}
</style>

