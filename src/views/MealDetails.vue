<template>
    <div class="max-w-[800px] mx-auto p-8">
        <h1 class="text-5xl font-bold mb-5img my-3"> {{ meal.strMeal }} </h1>
        <img :src="meal.strMealThumb" :alt="meal.strMeal">
        <div class="grid grid-cols-1 sm:grid-cols-3 text-lg py-2">
            <div>
                <strong class="font-bold">Catagory:</strong> {{meal.strCatagory}}
            </div>
            <div>
                <strong class="font-bold">Area:</strong> {{meal.strArea}}
            </div><div>
                <strong class="font-bold">Tags:</strong> {{meal.strTags}}
            </div>
        </div>
        <div class="my-3">
            {{ meal.strInstructions }}
        </div>
        <div class="grid grid-cols-1 sm:grid-cols-2">
            <div>
                <h2 class="text-2xl font-semibold mb-3">Ingredients</h2>
                <ul>
                    <template  v-for="(el, index) of new Array(20)">
                    <li v-if="meal[`strIngredient${index + 1}`]" :key="index">
                        {{  index + 1}}. {{ meal[`strIngredient${index + 1}`] }}
                    </li>
                    </template>
                </ul>
            </div>
             <div>
                <h2 class="text-2xl font-semibold mb-3">Measures</h2>
                <ul>
                    <template  v-for="(el, index) of new Array(10)">
                    <li v-if="meal[`strMeasure${index + 1}`]" :key="index">
                        {{ index + 1}}. {{ meal[`strMeasure${index + 1}`] }}
                    </li>
                    </template>
                </ul>
            </div>
            <div class="mt-3">
                <you-tube-button :href="meal.strYoutube" > Go to YouTube </you-tube-button>   
                <a
                    :href="meal.strSource"
                    target="_blank"
                    class="px-3 py-2 mx-4 rounded text-gray-700 border-2 border-indigo-600 bg-indigo-300 hover:bg-indigo-600 hover:text-white transition-colors">
                    
                    View Original Source
                </a>
            </div>
        </div>
    </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import { useRoute } from 'vue-router';
import axiosClient from '../axiosClient';
import YouTubeButton from '../components/YouTubeButton.vue'

const route = useRoute();
const meal = ref ({});


onMounted(() => {
 debugger
    axiosClient.get(`lookup.php?i=${route.params.id}`)
        .then(({ data }) => {
            meal.value = data.meals[0] || {};
        })
})
</script>

<style>

</style>