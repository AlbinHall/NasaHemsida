<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const prevDate = ref(new Date());
const endDate = ref(prevDate.value.toISOString().slice(0, 10));
const pictures = ref([]);

// Update prevDate and endDate on component mount
onMounted(async () => {
  prevDate.value.setDate(prevDate.value.getDate() - 6);
  const result = await axios.get(`https://api.nasa.gov/planetary/apod?api_key=HkCDh9mKfRedC5ZVCxbhmsiqWsr2UtFtUhahnuSO&start_date=${prevDate.value.toISOString().slice(0, 10)}&end_date=${endDate.value}`);
  pictures.value = result.data
});
</script>

<template>
   <div class="slider">
    <ul class="slides">
    <li v-for="pic in pictures.value">
        <img :src="pic.hdurl">
        <div class="caption center-align">
          <h3>This is our big Tagline!</h3>
          <h5 class="light grey-text text-lighten-3">Here's our small slogan.</h5>
        </div>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>