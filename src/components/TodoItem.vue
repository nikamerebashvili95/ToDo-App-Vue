<template>
  <li>
    <button
      @click="handleClick"
      :class="className"
      @dblclick="$emit('editItem')"
    >
      <i :class="{ circle: task.completed }" class="far fa-circle"></i
      >{{ task.title }}
    </button>
    <div class="btn-container">
      <button @click="$emit('editItem')">
        <i class="far fa-edit"></i>
      </button>
      <button @click="$emit('remove')">
        <i class="far fa-trash-alt"></i>
      </button>
    </div>
  </li>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["task"],
  data() {
    return {
      clickCount: 0,
    };
  },
  computed: {
    className() {
      let classes = ["toggle"];
      if (this.task.completed) {
        classes.push("toggle-completed");
      }
      return classes.join(" ");
    },
  },
  methods: {
    handleClick() {
      this.clickCount++;
      if (this.clickCount === 1) {
        setTimeout(() => {
          if (this.clickCount === 1) {
            this.$emit("complete");
          }
          this.clickCount = 0;
        }, 200);
      } else if (this.clickCount === 2) {
        this.clickCount = 0;
      }
    },
  },
};
</script>
