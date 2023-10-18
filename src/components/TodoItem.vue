<template>
  <li>
    <button
      @click.self="$emit('complete')"
      :class="className"
      @dblclick="$emit('editItem')"
    >
      <i class="far fa-circle"></i>{{ task.title }}
    </button>

    <div class="btn-container">
      <button @click="$emit('editItem')">
        <i class="far fa-edit"></i>
      </button>
      <button @click="$emit('remove')"><i class="far fa-trash-alt"></i></button>
    </div>
  </li>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["task"],
  computed: {
    className() {
      let classes = ["toggle"];
      if (this.task.completed) {
        classes.push("toggle-completed");
      }
      return classes.join(" ");
    },
  },
};
</script>
