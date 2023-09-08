<script setup>
import { computed } from "vue"

const props = defineProps({
  todos: {
    type: Array,
    required: true,
    default: [],
  },
})

const toDoCount = computed(() => props.todos.length)
const noToDo = computed(() => toDoCount.value === 0)
</script>

<template>
  <h3 v-if="noToDo">目前無任何ToDoList</h3>
  <h3 v-else>目前共計 {{ toDoCount }} 項 ToDoList</h3>
</template>
