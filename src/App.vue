
<script setup lang="ts">
import { reactive, ref } from 'vue';
import { items } from './assets/movies.json';
import { StarIcon } from "@heroicons/vue/24/solid";

import MovieForm from './components/MovieForm.vue';

const movies = ref(items);
const newMovie = ref({
    name: '',
    rating: 0,
    image: '',
    genres: '',
    description: ''
});

interface Movie {
    id: number;
    name: string;
    rating: number;
    image: string;
    genres: string[];
    description: string;
    inTheaters: boolean;
}



const isVisible = ref(false);

const handleForm = () => {
    isVisible.value = !isVisible.value;
}
function handleClick({ id, rating }: Pick<Movie, 'id' | 'rating'>): void {
    console.log('clicked', id, rating);
    const movie = movies.value.find(movie => movie.id === id);
    if (movie) {
        movie.rating = rating;
    }
}

function addMovie() {
    // Generate a new ID for the movie
    const newId = Math.max(...movies.map(movie => movie.id)) + 1;

    // Add the new movie to the list
    movies.push({
        id: newId,
        name: newMovie.name,
        rating: newMovie.rating,
        image: newMovie.image,
        genres: newMovie.genres.split(',').map(genre => genre.trim()),
        description: newMovie.description,
        inTheaters: false
    });

    // Reset the form
    newMovie.name = '';
    newMovie.rating = 1;
    newMovie.image = '';
    newMovie.genres = '';
    newMovie.description = '';
}

function updateRating(movie: any, newRating: any) {
    movie.rating = newRating;
}
</script>


<template>
    <!-- App container -->
    <div class="max-w-full flex items-center justify-center h-screen mx-auto app">
        <!-- Movie list -->
        <div class="flex items-center space-x-4">
            <!-- Movie item -->
            <div v-for="movie in movies" :key="movie.id"
                class="w-96 h-auto bg-white rounded-md flex flex-col items-center justify-start overflow-hidden shadow-2xl movie-item">
                <!-- Movie item image wrapper -->
                <div class="h-[520px] overflow-hidden w-full relative">
                    <!-- star icon wrapper for top right corner -->
                    <div class="absolute top-0 right-0">
                        <!-- set above image -->
                        <StarIcon class="h-16 w-16" :class="[movie.rating ? 'text-yellow-600' : 'text-gray-500']" />
                        <div class="absolute inset-0 flex items-center justify-center text-center">
                            <span v-if="movie.rating" class="text-xl text-yellow-800">{{ movie.rating }}</span>
                            <span v-else class="text xl-text-yellow-400">-</span>
                        </div>
                    </div>
                    <img :src="movie.image" alt="" class="object-cover object-center h-[600px]" />
                </div>
                <!-- Card content wrapper -->
                <div class="h-56 p-4 flex flex-col items-start justify-start w-full">
                    <!-- Movie item title wrapper -->
                    <div class="h-16 w-full">
                        <h3 class="text-2xl">{{ movie.name }}</h3>
                        <!-- Wrapper for genres -->
                        <div class="flex items-center justify-start pt-2 space-x-1">
                            <span v-for="genre in movie.genres" :key="`${movie.id}-${genre}`"
                                class="text-xs bg-indigo-500 text-white py-0.5 px-2 rounded-full">{{ genre }}</span>
                        </div>
                    </div>
                    <!-- Movie item description wrapper -->
                    <div class="h-24 flex-1 pl-0.5 pt-1">
                        <p class="text-sm">{{ movie.description }}</p>
                    </div>
                    <!-- Rating -->
                    <div class="w-full flex items-center justify-start h-8">
                        <span class="text-xs mr-2 leading-7">
                            Rating: {{ movie.rating }} / 5
                        </span>
                        <button v-for="starIndex in 5" :key="`${movie.id}-${starIndex}`"
                            :class="[{ 'opacity-75 cursor-not-allowed': starIndex == movie.rating },
                            { 'text-yellow-500': starIndex <= movie.rating, 'text-gray-400': starIndex > movie.rating }]" :disabled="starIndex == movie.rating"
                            @click="handleClick({ id: movie.id, rating: starIndex })">
                            <StarIcon
                                :class="[{ 'text-yellow-500': starIndex <= movie.rating, 'text-gray-400': starIndex > movie.rating }, { 'opacity-75 cursor-not-allowed': starIndex == movie.rating }]"
                                class="h-5 w-5" />
                        </Button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

  
  
<style lang="scss" scoped>
/* Add your custom styles here */
</style>