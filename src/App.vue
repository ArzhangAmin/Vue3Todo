<template>
  <app-header></app-header>
  <main>
    <add-todo v-on:AddNewTodo="handleAddTodo"></add-todo>
    <ul class="todos">
      <todo
        v-for="(item, i) in getTodo"
        :key="item.id"
        :todo="item"
        @dragstart="dragStart(i)"
        @onDeleted="DeleteTodo"
        @changeStatus="changeTodoStatus"
        @dragover.prevent
        @drop="drop(i)"
      ></todo>
    </ul>
    <div class="card stat">
      <p class="corner">
        <span id="items-left">{{ getActiveTodoCount }}</span> items left
      </p>
      <div class="filter">
        <button
          id="all"
          :class="{ on: activeTab == 'all' }"
          @click="changeTab('all')"
        >
          All
        </button>
        <button
          id="active"
          :class="{ on: activeTab == 'active' }"
          @click="changeTab('active')"
        >
          Active
        </button>
        <button
          id="completed"
          :class="{ on: activeTab == 'completed' }"
          @click="changeTab('completed')"
        >
          Completed
        </button>
      </div>
      <div class="corner">
        <button @click="deleteCompleted" id="clear-completed">
          Clear Completed
        </button>
      </div>
    </div>
  </main>
  <app-footer></app-footer>
</template>

<script setup>
import AppHeader from "./components/AppHeader.vue";
import AppFooter from "./components/AppFooter.vue";
import AddTodo from "./components/AddTodo.vue";
import Todo from "./components/Todo.vue";
import { ref, computed } from "vue";
import { useToast } from "vue-toastification";

var todos = ref([]);
const dragging = ref(-1);
const activeTab = ref("all");
const toast = useToast();

const getActiveTodoCount = computed(() => {
  return todos.value.filter((f) => f.isComplete == false).length;
});

const getTodo = computed(() => {
  switch (activeTab.value) {
    case "all":
      return todos.value;
    case "active":
      return todos.value.filter((f) => f.isComplete == false);
    case "completed":
      return todos.value.filter((f) => f.isComplete == true);
    default:
      return todos.value;
  }
});

function handleAddTodo(title) {
  if (!title) {
    toast.error("Enter a title");
    return;
  }
  const id = Math.random().toString(16).slice(2);
  const todo = { id, title, isComplete: false };
  todos.value.push(todo);
  toast.success("Task added successfully");
}
function DeleteTodo(id) {
  const todo = todos.value.find((f) => f.id == id);
  todos.value = todos.value.filter((f) => f.id !== id);
  toast.error(`${todo.title} deleted successfully`);
}
function changeTodoStatus(id, newStatus) {
  var newTodos = [...todos.value];
  var selectedTodo = newTodos.find((f) => f.id === id);
  selectedTodo.isComplete = newStatus;
  todos.value = newTodos;
}
function deleteCompleted() {
  if (confirm("Are you sure you want to delete completed tasks?")) {
    var newTodos = [...todos.value];
    newTodos = newTodos.filter((f) => f.isComplete === false);
    todos.value = newTodos;
    toast.success("Completed tasks deleted successfully");
  }
}
function dragStart(index) {
  dragging.value = index;
}
function drop(index) {
  var newElement = todos.value.splice(dragging.value, 1)[0];
  todos.value.splice(index, 0, newElement);
}
function changeTab(tab) {
  activeTab.value = tab;
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
