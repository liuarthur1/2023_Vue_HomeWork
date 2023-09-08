<script setup>
import TodoCount from "@/components/headers/TodoCount.vue"
import TodoItem from "@/components/toDOLists/Item.vue"
import { v4 as uuidv4 } from "uuid"
import { ref, reactive, onBeforeMount } from "vue"

const newTodo = ref("")
const toDoList = reactive([])

const addTodo = () => {
  if (newTodo.value !== "") {

    // console.log("addTodo trigger!!")
    const todo = {
      id: uuidv4(),
      title: newTodo.value,
      completed: false,
    }
    toDoList.unshift(todo)

    // console.log(device.value)
    // save(StorageKey, devices)

    newTodo.value = ""
  }
}

const removeItem = (id) => {
  const index = toDoList.findIndex((todo) => {
    return todo.id === id
  })

  toDoList.splice(index, 1)
  // save(StorageKey, devices)
}
</script>

<template>
  <main class="container mx-auto">
    <header class="m-2">
      <h1 class="text-6xl font-thin select-none">TODO!</h1>
      <div class="font-semibold select-none text-neutral-600">simple and studid todo app</div>
    </header>
    <form class="px-10 py-12 bg-white shadow-sm">
      <section class="flex">
        <input
          type="text"
          placeholder="做點重要的事吧..."
          class="w-full text-2xl focus:outline-none input-lg input input-bordered"
          v-model="newTodo"
        />
        <button @click.prevent="addTodo" class="text-xl btn-lg btn btn-neutral">新增</button>
      </section>
    </form>

    <section class="px-10 py-6 mt-4 bg-white">
      <header>
        <TodoCount :todos="toDoList" />
      </header>

      <ul>
        <TodoItem @remove-toDo-item="removeItem" v-for="todo in toDoList" :todo="todo" />
      </ul>
    </section>

    
  </main>
</template>

<style scoped></style>
