<template>
  <li>
    <button class="toggle">
      <i class="far fa-circle"></i>{{ task.title }}
    </button>
    <button><i class="far fa-trash-alt"></i></button>
  </li>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["task"],
};
</script>
