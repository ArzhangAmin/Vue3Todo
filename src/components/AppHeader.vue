<template>
  <header class="card">
    <h1>Task List</h1>
    <button id="theme-switcher" @click="changeTheme">
      <img v-if="defaultTheme == 'dark'" :src="Sun" alt="Change color theme" />
      <img v-else :src="Moon" alt="Change color theme" />
    </button>
  </header>
</template>

<script setup>
import Sun from "../assets/icon-sun.svg";
import Moon from "../assets/icon-moon.svg";
import { ref } from "vue";

const defaultTheme = ref("dark");

const changeTheme = () => {
  if (defaultTheme.value == "dark") {
    defaultTheme.value = "light";
    document.querySelector("body").classList.add("light");
  } else {
    defaultTheme.value = "dark";
    document.querySelector("body").classList.remove("light");
  }
};
</script>
