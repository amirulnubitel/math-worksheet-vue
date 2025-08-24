<template>
  <div class="question-card animate-fade-in">
    <h3 class="text-lg font-semibold text-gray-800 mb-4">
      {{ questionNumber }}. {{ question.text }}
    </h3>
    
    <div class="space-y-3">
      <div
        v-for="(option, index) in question.options"
        :key="index"
        class="option-button"
        :class="{ selected: selectedAnswer === option }"
        @click="selectOption(option)"
      >
        <span class="flex items-center">
          <span
            class="inline-block w-4 h-4 rounded-full border-2 mr-3 transition-colors duration-200"
            :class="selectedAnswer === option 
              ? 'bg-blue-500 border-blue-500' 
              : 'border-gray-400'"
          ></span>
          {{ option }}
        </span>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
interface Question {
  text: string
  options: (string | number)[]
  correctAnswer: string | number
}

interface Props {
  question: Question
  questionNumber: number
  modelValue?: string | number
}

interface Emits {
  (e: 'update:modelValue', value: string | number): void
}

const props = defineProps<Props>()
const emit = defineEmits<Emits>()

const selectedAnswer = computed({
  get: () => props.modelValue,
  set: (value) => emit('update:modelValue', value)
})

const selectOption = (option: string | number) => {
  selectedAnswer.value = option
}
</script>