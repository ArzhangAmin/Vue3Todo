<template>
  <div class="card add">
    <div class="cb-container">
      <button id="add-btn" @click="AddTodo">+</button>
    </div>
    <div class="txt-container">
      <label for="addt">Add </label>
      <input
        v-model="todoTitle"
        type="text"
        class="txt-input"
        placeholder="Add new Task..."
        spellcheck="false"
        autocomplete="off"
        id="addt"
        dir="ltr"
        @keypress.enter="AddTodo"
      />
    </div>
  </div>
</template>

<script setup>
import { ref, defineEmits } from "vue";

const todoTitle = ref("");
const emits = defineEmits(["AddNewTodo"]);

function AddTodo() {
  emits("AddNewTodo", todoTitle.value);
  todoTitle.value = "";
}
</script>

<style></style>
