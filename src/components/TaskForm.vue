<script setup lang="ts">
import { ref } from 'vue'
const newTask = ref('')
const error = ref('')

const emit = defineEmits<{ addTask: [newTask: string] }>()

const handleSubmit = async () => {
  if (newTask.value.trim()) {
    emit('addTask', newTask.value)
    newTask.value = ''
  } else {
    error.value = 'Task cant be empty'
  }
}
</script>

<template>
  <form @submit.prevent="handleSubmit">
    <label for="newTask">New Task</label>
    <input
      @input="error = ''"
      v-model="newTask"
      :aria-invalid="!!error || undefined"
      type="text"
      name="newTask"
    />
    <small v-if="error" id="invalid-helper">
      {{ error }}
    </small>
    <div class="button-container">
      <button>Add</button>
    </div>
  </form>
</template>
