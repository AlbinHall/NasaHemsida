<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const prevDate = ref(new Date());
const endDate = ref(new Date());
const pictures = ref([]);

// Update prevDate and endDate on component mount
onMounted(async () => {
  prevDate.value.setDate(prevDate.value.getDate() - 7);
  endDate.value.setDate(endDate.value.getDate() - 1);
  const result = await axios.get(`https://api.nasa.gov/planetary/apod?api_key=HkCDh9mKfRedC5ZVCxbhmsiqWsr2UtFtUhahnuSO&start_date=${prevDate.value.toISOString().slice(0, 10)}&end_date=${endDate.value.toISOString().slice(0, 10)}`);
  pictures.value = result.data
});

</script>

<template>
  <div class="row row-cols-1 row-cols-md-3 g-4">
    <div v-for="picture in pictures" class="col">
      <div class="card" style="width: 18rem;">
        <img :src="picture.hdurl" class="card-img-top space-pic">
        <div class="card-body">
          <div data-bs-theme="dark" class="dropdown">
            <button class="btn btn-secondary  dropdown-toggle" type="button" data-bs-toggle="dropdown" aria-expanded="false">
              More info
            </button>
            <ul class="dropdown-menu">
              <li><p class="card-text">{{ picture.explanation }}</p></li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>