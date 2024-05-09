<template>
  <div class="flex flex-col  justify-center items-center  w-100 p-8  ">
  Welcome Random Meals Page ~ Go to the relevant menu
  </div>

</template>

<script setup>
import { computed, onMounted, ref } from 'vue';
import  store  from '../store';
import axiosClient from '../axiosClient';

const ingredients = ref([]);


const meals = computed(() => store.state.meals );

onMounted(async () => {
  const response = await axiosClient.get('/list.php?i=list')
  console.log(response.data);
  ingredients.value = response.data;
})


</script>
