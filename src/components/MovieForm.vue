<script setup lang="ts">

const emit = defineEmits(['create', 'close'])

</script>

<template>
    <form @submit.prevent="emit('create')">
        <div class="backdrop-blur-xl flex px-16 rounded-md flex-col items-center mt-8 justify-center text-center text-gray">
            <div class="flex flex-col mb-4">
                <label for="name" class="text-white text-lg font-semibold mb-2">Name</label>
                <input type="text" id="name" class="border border-gray-400 p-2 rounded-lg" required>
            </div>

            <div class="flex flex-col mb-4">
                <label for="rating" class="text-white text-lg font-semibold mb-2">Rating</label>
                <input type="number" id="rating" class="border border-gray-400 p-2 rounded-lg" min="1" max="5" required>
            </div>

            <div class="flex flex-col mb-4 ">
                <label for="image" class="text-white text-lg font-semibold mb-2">Image URL</label>
                <input type="url" id="image" class="border border-gray-400 p-2 rounded-lg" required>
            </div>

            <div class="flex flex-col mb-4 ">
                <label for="genres" class="text-white text-lg font-semibold mb-2">Genres (comma-separated)</label>
                <input type="text" id="genres" class="border border-gray-400 p-2 rounded-lg" required>
            </div>

            <div class="flex flex-col mb-4">
                <label for="description" class="text-white text-lg font-semibold mb-2">Description</label>
                <textarea id="description" class="border border-gray-400 p-2 rounded-lg" required></textarea>
            </div>

            <button type="submit" @click="emit('close')"
                class="bg-blue-500 text-white py-2 px-4 rounded-lg hover:bg-blue-600">
                Add movie
            </button>
        </div>
    </form>
</template>
<style lang="scss" scoped></style>