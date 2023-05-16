<template>
	<div class="mb-6">
		<label class="block mb-2 text-sm font-medium text-gray-700" for="weight">Weight (kg):</label>
		<input v-model="weight"
			class="w-full py-2 px-4 rounded border border-gray-300 focus:border-pink-500 focus:outline-none" id="weight"
			type="number" step="0.1" placeholder="Enter weight" required>
	</div>
	<div class="mb-6">
		<label class="block mb-2 text-sm font-medium text-gray-700" for="height">Height (cm):</label>
		<input v-model="height"
			class="w-full py-2 px-4 rounded border border-gray-300 focus:border-pink-500 focus:outline-none" id="height"
			type="number" step="0.01" placeholder="Enter height" required>
	</div>
	<div class="mb-6">
		<label class="block mb-2 text-sm font-medium text-gray-700">Gender:</label>
		<div class="flex justify-center">
			<label for="female" class="mr-2">
				<input type="radio" id="female" value="Female" v-model="genderVal" @change="selectGender">
				Female
			</label>
			<label for="male">
				<input type="radio" id="male" value="Male" v-model="genderVal" @change="selectGender">
				Male
			</label>
		</div>
	</div>
	<div class="mb-6">
		<button @click="calculateBMI"
			class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-8 rounded w-full transition duration-300"
			id="calculate-btn">Calculate BMI</button>
	</div>
</template>
<script setup>
import { ref } from 'vue';

const emit = defineEmits(['calculate', 'select-gender', 'reset']);
const weight = ref('');
const height = ref('');
const genderVal = ref('');

const selectGender = () => {
	emit('select-gender', genderVal.value);
};

const calculateBMI = () => {
	const weightValue = parseFloat(weight.value);
	const heightValue = parseFloat(height.value);
	const gender = genderVal.value;

	if (isNaN(weightValue) || isNaN(heightValue)) {
		emit('calculate', alert('Please fill in all fields the Blank.'));
	} else if (!gender) {
		emit('calculate', alert('Please Select the Gender.'));
	} else {
		emit('calculate', {
			weight: weightValue,
			height: heightValue,
			gender,
		});
	}
};

const resetForm = () => {
	weight.value = '';
	height.value = '';
	emit('reset');
};

emit('reset', resetForm);
</script>  