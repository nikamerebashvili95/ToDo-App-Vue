<template>
  <div>
    <h1>TodoList</h1>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";
import axios from "axios";
export default {
  components: {
    TodoItem,
  },
};
</script>
