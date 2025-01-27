<script setup>
import { ref } from "vue";

const url = "https://official-joke-api.appspot.com/";

const data = ref({});
const isRevealed = ref(false);

async function getData() {
  isRevealed.value = false;
  try {
    const response = await fetch(url + "jokes/random");
    data.value = await response.json();
    console.log(data.value);
  } catch (error) {
    console.log(error);
  }
}
</script>

<template>
  <h2>{{ data.setup }}</h2>
  <button
    v-if="data.setup && !isRevealed"
    @click="() => (isRevealed = !isRevealed)"
  >
    Reveal
  </button>
  <p>{{ isRevealed ? data.punchline : "" }}</p>

  <button @click="getData">New Joke</button>
</template>

<style scoped></style>
