<script setup>
import { ref, reactive } from "vue";
const msg = ref("Hello World");
const state = reactive({ count: 0 });
const increment = () => {
  state.count++;
};
</script>

<template>
  <h1>{{ msg }}</h1>
  <h2>{{ state.count }}</h2>
  <button @click="state.count++">Increment Count</button>
  <button @click="increment">Increment Count</button>
  <br />
  <input v-model="msg" />
</template>
