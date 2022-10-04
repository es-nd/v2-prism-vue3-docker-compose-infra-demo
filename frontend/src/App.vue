<script setup lang="ts">
import { ref } from 'vue';
import axios from "axios";
import { SampleApiFactory, Configuration } from "./api/generated";
import HelloWorld from './components/HelloWorld.vue'

const text = ref('');

const sampleApi = SampleApiFactory(
  new Configuration({ basePath: import.meta.env.VITE_API_BASE_URL }),
  undefined,
  axios.create()
);

const getSample = async () => {
  const response = await sampleApi.getSample();
  text.value = response.data.text;
}
getSample();
</script>

<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld :msg="text" />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
