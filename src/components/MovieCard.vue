<script setup lang="ts">

interface Props {
    id: number;
    name: string;
    description: string;
    genres: any;
    rating: number;
}

const movie = defineProps<Props>();

</script>


<template>
    <div class="p-3">
        <h2 class="text-xl font-semibold pb-1">{{ movie.name }}</h2>

        <div class="text-sm inline">
            <span class="genre-tag" v-for="genre in movie.genres" :key="genre">{{ genre }}</span>
        </div>

        <div class="">
            <p class="pt-3 text-sm">{{ movie.description }}</p>
        </div>

        <div class="pt-6 leading-7">
            Rating: {{ movie.rating }} / 5
            <button v-for="rating in 5" :key="rating" class="movie-star-icon pt-2" @click="updateRating(movie, rating)"
                :disabled="rating === movie.rating">
                <StarIcon :class="{
                    'text-yellow-500': rating <= movie.rating,
                    'text-gray-400': rating > movie.rating,
                    'cursor-pointer': rating !== movie.rating

                }" class="pt-2 w-6 h-6" />
            </button>
        </div>
    </div>
</template>

<style lang="scss" scoped></style>