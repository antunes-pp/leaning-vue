<script setup lang="ts">
import { reactive, ref } from 'vue'

const count = ref(0)

const tasks = reactive<Array<{ label: string; id: string; isDone: boolean }>>([])
const taskName = ref<string>('')

function onSubmit() {
  if (!taskName.value) {
    return
  }

  tasks.push({ id: taskName.value, label: taskName.value, isDone: false })

  taskName.value = ''
}

function toggleTask(idx: number) {
  tasks[idx].isDone = !tasks[idx].isDone
}
</script>

<template>
  <main class="container">
    <header>
      <h1>Hello world: {{ count }} 👍</h1>
    </header>

    <form @submit.prevent="onSubmit">
      <input placeholder="New task" v-model.lazy="taskName" />

      <span>
        {{ taskName }}
      </span>
    </form>

    <button @click="count++">incressing</button>

    <ul v-if="tasks.length" class="tasks-container">
      <li
        v-for="(task, index) in tasks"
        class="task"
        :key="task.id"
        @click="toggleTask(index)"
        :class="{
          done: task.isDone
        }"
      >
        {{ task.label }} - {{ index }}

        <span v-if="task.isDone">doned</span>
      </li>
    </ul>
  </main>
</template>

<style lang="css" scoped>
.container {
  width: 100%;
  max-width: 720px;
  margin: 0 auto;
  padding: 1rem;
}

.tasks-container {
  margin-top: 30px;
  display: flex;
  flex-direction: column;
  list-style: none;
}

.task {
  font-size: 1rem;
}

.task.done {
  color: green;
  text-decoration: line-through;
}
</style>
