<template>
  <div class="container">
    <div class="task">
      <!-- title -->
      <div class="title">
        <h1>To Do App</h1>
      </div>
      <!-- form -->
      <div class="form">
        <input type="text" placeholder="New Task" />
        <button><i class="fas fa-plus"></i></button>
      </div>
      <!-- task lists -->
      <div class="taskItems">
        <ul>
          <li>
            <button class="toggle">
              <i class="far fa-circle"></i>Learn Vue JS
            </button>
            <button><i class="far fa-trash-alt"></i></button>
          </li>
          <li>
            <button class="toggle">
              <i class="far fa-circle"></i>Watch netflix
            </button>
            <button><i class="far fa-trash-alt"></i></button>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";

export default {
  components: {
    TodoItem,
  },
};
</script>
