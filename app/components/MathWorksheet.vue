<template>
	<div class="bg-white rounded-lg shadow-xl p-8">
		<!-- Header -->
		<div class="text-center mb-8">
			<h1 class="text-3xl font-bold text-gray-800 mb-2">Math Worksheet</h1>
			<h2 class="text-xl text-gray-600 mb-4">Rounding Off to Nearest 10</h2>
			<p class="text-gray-500 text-sm">Complete all questions and enter your name to get your score</p>
		</div>

		<!-- Name Input -->
		<div class="mb-8">
			<label for="name" class="block text-sm font-medium text-gray-700 mb-2"> Name <span class="text-red-500">*</span> </label>
			<input id="name" v-model="name" type="text" placeholder="Enter your name" class="input-field" :class="{ 'border-red-500 focus:ring-red-500 focus:border-red-500': nameError }" />
			<p v-if="nameError" class="error-message">{{ nameError }}</p>
		</div>

		<!-- Questions Grid -->
		<div class="grid gap-6 md:grid-cols-1 lg:grid-cols-2 mb-8">
			<QuestionItem v-for="(question, index) in questions" :key="index" :question="question" :question-number="index + 1" v-model="answers[index]" />
		</div>

		<!-- Action Buttons -->
		<div class="flex flex-col sm:flex-row gap-4 justify-center mb-6">
			<button @click="resetWorksheet" class="btn-secondary">Reset All Answers</button>
			<button @click="submitWorksheet" :disabled="!canSubmit" class="btn-primary">Submit & Get Score</button>
		</div>

		<!-- Score Display -->
		<div v-if="showScore" class="score-display">
			<h3 class="text-2xl font-bold text-green-700 mb-2">Great Job, {{ name }}!</h3>
			<p class="text-xl text-green-600 mb-2">Your Score: {{ score }}/{{ questions.length }}</p>
			<p class="text-lg text-gray-600">
				{{ getScoreMessage() }}
			</p>
			<div class="mt-4">
				<div class="w-full bg-gray-200 rounded-full h-3">
					<div class="bg-green-500 h-3 rounded-full transition-all duration-1000 ease-out" :style="{ width: `${(score / questions.length) * 100}%` }"></div>
				</div>
			</div>
		</div>

		<!-- Copyright -->
		<div class="text-center text-xs text-gray-400 mt-8 pt-4 border-t border-gray-200">© 2024 Math Worksheet Application. All rights reserved.</div>
	</div>
</template>

<script setup lang="ts">
interface Question {
	text: string;
	options: (string | number)[];
	correctAnswer: string | number;
}

// Questions data with correct answers
const questions: Question[] = [
	{
		text: "17 rounded off to the nearest 10 is...",
		options: [10, 20, 17],
		correctAnswer: 20,
	},
	{
		text: "45 rounded off to the nearest 10 is...",
		options: [50, 45, 40],
		correctAnswer: 50,
	},
	{
		text: "75 rounded off to the nearest 10 is...",
		options: [70, 80, 175],
		correctAnswer: 80,
	},
	{
		text: "19 rounded to the nearest 10 is...",
		options: [20, 10, 19],
		correctAnswer: 20,
	},
	{
		text: "64 rounded off to the nearest 10 is...",
		options: [64, 70, 60],
		correctAnswer: 60,
	},
	{
		text: "6 rounded off to the nearest 10 is...",
		options: [10, 1, 0],
		correctAnswer: 10,
	},
	{
		text: "98 rounded off to the nearest 10 is...",
		options: [80, 100, 89],
		correctAnswer: 100,
	},
	{
		text: "199 rounded off to the nearest 10 is...",
		options: [190, 100, 200],
		correctAnswer: 200,
	},
	{
		text: "94 rounded off to the nearest 10 is...",
		options: [100, 94, 90],
		correctAnswer: 90,
	},
	{
		text: "165 rounded off to the nearest 10 is...",
		options: [160, 170, 150],
		correctAnswer: 170,
	},
	{
		text: "445 rounded off to the nearest 10 is...",
		options: [450, 440, 500],
		correctAnswer: 450,
	},
	{
		text: "999 rounded off to the nearest 10 is...",
		options: [990, "1,000", 909],
		correctAnswer: "1,000",
	},
];

// Reactive state
const name = ref("");
const answers = ref<(string | number | undefined)[]>(new Array(questions.length).fill(undefined));
const showScore = ref(false);
const score = ref(0);
const nameError = ref("");

// Computed properties
const canSubmit = computed(() => {
	return name.value.trim() !== "" && answers.value.every((answer) => answer !== undefined);
});

const allQuestionsAnswered = computed(() => {
	return answers.value.every((answer) => answer !== undefined);
});

// Methods
const validateName = (): boolean => {
	if (name.value.trim() === "") {
		nameError.value = "Please enter your name before submitting";
		return false;
	}
	nameError.value = "";
	return true;
};

const calculateScore = (): number => {
	let correctCount = 0;
	answers.value.forEach((answer, index) => {
		if (answer === questions[index].correctAnswer) {
			correctCount++;
		}
	});
	return correctCount;
};

const getScoreMessage = (): string => {
	const percentage = (score.value / questions.length) * 100;
	if (percentage === 100) return "Perfect! You got all questions correct!";
	if (percentage >= 80) return "Excellent work! You're doing great!";
	if (percentage >= 60) return "Good job! Keep practicing!";
	if (percentage >= 40) return "Not bad! You can improve with more practice!";
	return "Keep trying! Practice makes perfect!";
};

const submitWorksheet = () => {
	// Validate name
	if (!validateName()) {
		return;
	}

	// Check if all questions are answered
	if (!allQuestionsAnswered.value) {
		alert("Please answer all questions before submitting");
		return;
	}

	// Calculate and show score
	score.value = calculateScore();
	showScore.value = true;

	// Scroll to score section
	nextTick(() => {
		const scoreElement = document.querySelector(".score-display");
		if (scoreElement) {
			scoreElement.scrollIntoView({ behavior: "smooth" });
		}
	});
};

const resetWorksheet = () => {
	if (confirm("Are you sure you want to reset all answers and start over?")) {
		name.value = "";
		answers.value = new Array(questions.length).fill(undefined);
		showScore.value = false;
		score.value = 0;
		nameError.value = "";
	}
};

// Watch for name changes to clear errors
watch(name, () => {
	if (nameError.value && name.value.trim() !== "") {
		nameError.value = "";
	}
});
</script>
