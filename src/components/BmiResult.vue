<template>
    <div class="text-center">
        <h2 class="text-2xl font-bold mb-2">Your BMI: {{ bmi }}</h2>
        <p v-if="category" class="mb-2">Category: {{ category }}</p>
        <p v-if="category && gender" class="mb-2">Your gender is: {{ gender }}</p>
        <button @click="resetBMI"
            class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-8 rounded w-full transition duration-300">
            Reset
        </button>
    </div>
</template>
  
<script setup>
import { defineProps } from 'vue';

defineProps({
    bmi: {
        type: Number,
        required: true,
    },
    category: {
        type: String,
        default: '',
    },
    gender: {
        type: String,
        default: '',
    },
});

const emit = defineEmits(['reset']);

const resetBMI = () => {
    emit('reset');
};
</script>