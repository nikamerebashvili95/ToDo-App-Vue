<template>
  <div>
    <h1>TodoItem</h1>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: {
    name: String,
    completed: Boolean,
  },
};
</script>
