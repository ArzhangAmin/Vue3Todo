<template>
  <li class="card" draggable="true">
    <div class="cb-container">
      <input
        type="checkbox"
        :checked="todo.isComplete ? true : null"
        class="cb-input"
        @click="changeStatus"
      />
      <span class="check"></span>
    </div>
    <p class="item">
      <del v-if="todo.isComplete == true">{{ todo.title }}</del>
      <span v-else v-text="todo.title"></span>
    </p>
    <button class="clear" @click="deleteTodo">
      <img :src="Cross" alt="Clear it" />
    </button>
  </li>
</template>

<script setup>
import Cross from "../assets/icon-cross.svg";
import { defineProps, toRef, defineEmits } from "vue";

const props = defineProps({
  todo: Object,
});
const emits = defineEmits(["onDeleted", "changeStatus"]);

const todo = toRef(props, "todo");

function deleteTodo() {
  if (confirm("Are you sure you want to delete this task?")) {
    emits("onDeleted", todo.value.id);
  }
}
function changeStatus() {
  emits("changeStatus", todo.value.id, !todo.value.isComplete);
}
</script>
