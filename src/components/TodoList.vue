<template>
  <div class="container">
    <div class="task">
      <!-- title -->
      <div class="title">
        <h1>To Do App</h1>
      </div>
      <!-- form -->
      <div class="form">
        <input
          type="text"
          placeholder="New Task"
          v-model="newTask"
          @keyup.enter="addTask"
        />
        <button @click="addTask"><i class="fas fa-plus"></i></button>
      </div>
      <!-- task lists -->
      <div class="taskItems">
        <ul>
          <TodoItem
            v-bind:task="task"
            v-for="(task, index) in tasks"
            :key="task.id"
            @remove="removeTask(index)"
            @complete="completeTask(task)"
            @editItem="editTask(index)"
          />
        </ul>
      </div>
      <!-- buttons -->
      <div class="clearBtns">
        <button @click="clearCompleted">Clear completed</button>
        <button @click="clearAll">Clear all</button>
      </div>
      <!-- pending task -->
      <div class="pendingTasks">
        <span>Pending Tasks: {{ incomplete }} </span>
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
      newTask: "",
      maxTasksToShow: 10,
      editingIndex: null,
    };
  },
  computed: {
    incomplete() {
      return this.tasks.filter(this.inProgress).length;
    },
  },
  methods: {
    addTask() {
      if (this.newTask) {
        if (this.editingIndex !== null) {
          this.tasks[this.editingIndex].title = this.newTask;
          this.editingIndex = null;
        } else {
          this.tasks.push({
            title: this.newTask,
            completed: false,
          });
        }
        this.newTask = "";
        this.saveTasksToLocalStorage();
      }
    },
    inProgress(task) {
      return !this.isCompleted(task);
    },
    isCompleted(task) {
      return task.completed;
    },
    clearCompleted() {
      this.tasks = this.tasks.filter(this.inProgress);
      this.saveTasksToLocalStorage();
    },
    clearAll() {
      this.tasks = [];
      this.saveTasksToLocalStorage();
    },
    completeTask(task) {
      task.completed = !task.completed;
      this.editingIndex = null;
      this.saveTasksToLocalStorage();
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
      this.editingIndex = null;
      this.saveTasksToLocalStorage();
    },
    editTask(index) {
      if (!this.tasks[index].completed) {
        this.newTask = this.tasks[index].title;
        this.editingIndex = index;
      }
    },
    saveTasksToLocalStorage() {
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
  },
  mounted() {
    const savedTasks = localStorage.getItem("tasks");
    if (savedTasks) {
      this.tasks = JSON.parse(savedTasks);
    } else {
      axios
        .get("https://jsonplaceholder.typicode.com/todos")
        .then((response) => {
          this.tasks = response.data.slice(0, this.maxTasksToShow);
          this.saveTasksToLocalStorage();
        })
        .catch((error) => {
          console.error("Error fetching todos:", error);
        });
    }
  },
};
</script>
