<script setup lang="ts">
import TodoList from "./components/TodoList.vue";
import NavbarComponent from "./components/NavbarComponent.vue";
import TableComponent from "./components/TableComponent.vue";
</script>

<template>
  <NavbarComponent />
  <div class="space-y-7">
    <TodoList />
  </div>
</template>

<style scoped></style>
