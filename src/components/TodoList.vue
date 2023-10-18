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
          <li v-for="task in tasks" :key="task.id">
            <button class="toggle">
              <i class="far fa-circle"></i>{{ task.title }}
            </button>
            <button><i class="far fa-trash-alt"></i></button>
          </li>
        </ul>
      </div>
      <!-- buttons -->
      <div class="clearBtns">
        <button>Clear completed</button>
        <button @click="clearAll">Clear all</button>
      </div>
      <!-- pending task -->
      <div class="pendingTasks">
        <span>Pending Tasks: </span>
      </div>
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";
import axios from "axios";
export default {
  components: {
    TodoItem,
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    clearAll() {
      this.tasks = [];
    },
  },
  mounted() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos")
      .then((response) => {
        this.tasks = response.data;
        console.log(response.data);
      })
      .catch((error) => {
        console.error("Error fetching todos:", error);
      });
  },
};
</script>
