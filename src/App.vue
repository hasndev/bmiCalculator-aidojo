<template>
  <div class="flex items-center justify-center h-screen">
    <div class="card shadow-dark-50 bg-[#ffbb00e7] p-8 rounded-lg">
      <h2 class="text-4xl text-center mb-8 font-semibold text-gray-800">BMI Calculator</h2>
      <BMIForm :weight="weightVal" :height="heightVal" :gender="genderVal" :selectedGender="selectedGender"
        @calculate="calculateBMI" @select-gender="selectGender" @reset="resetBMI"></BMIForm>
      <BMIResult v-if="bmi !== null" :bmi="bmi" :category="bmiCategory" :gender="selectedGender" @reset="resetBMI">
      </BMIResult>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';
import BMIForm from '@/components/BmiForm.vue';
import BMIResult from '@/components/BmiResult.vue';

const weightVal = ref('');
const heightVal = ref('');
const genderVal = ref('');
const bmiVal = ref(null);
const selectedGender = ref('');

const calculateBMI = ({ weight, height, gender }) => {
  if (isNaN(weight) || isNaN(height) || !gender) {
    bmiVal.value = null;
  } else {
    const bmi = weight / ((height / 100) * (height / 100));
    bmiVal.value = bmi.toFixed(2);
  }
};

const bmiCategory = computed(() => {
  if (bmiVal.value === null) {
    return '';
  } else if (bmiVal.value < 18.5) {
    return 'Underweight';
  } else if (bmiVal.value < 25) {
    return 'Normal weight';
  } else if (bmiVal.value < 30) {
    return 'Overweight';
  } else {
    return '';
  }
});

const selectGender = (gender) => {
  selectedGender.value = gender;
  genderVal.value = gender;
};

const bmi = computed(() => bmiVal.value);

const resetBMI = () => {
  weightVal.value = '';
  heightVal.value = '';
  genderVal.value = '';
  bmiVal.value = null;
  selectedGender.value = '';
};

onMounted(() => {
  document.getElementById('weight').focus();
});
</script>
