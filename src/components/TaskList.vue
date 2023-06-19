<template>
  <div>
    <h2>Task List</h2>
    <ul>
      <task-item
        v-for="task in sortedTasks"
        :key="task.id"
        :task="task"
        @toggleStatus="toggleTaskStatus(task)"
        @deleteTask="deleteTask(task)"
        @editTask="editTask(task)"
        @changePriority="changePriority(task)"
        ><h1>{{ task.priority }}</h1>

      </task-item>
    </ul>
    <p>Total Tasks: {{ totalTasks }}</p>
    <p id="green">Completed Tasks: {{ completedTasks }}</p>
  </div>
</template>

<script>
import TaskItem from "./TaskItem.vue";

export default {
  components: {
    TaskItem,
  },
  data() {
    return {
      tasks: [],
    };
  },
  computed: {
    totalTasks() {
      return this.tasks.length;
    },
    completedTasks() {
      return this.tasks.filter((task) => task.completed).length;
    },
    sortedTasks() {
      const highPriorityTasks = this.tasks.filter(task => task.priority === 'high');
      const mediumPriorityTasks = this.tasks.filter(task => task.priority === 'medium');
      const lowPriorityTasks = this.tasks.filter(task => task.priority === 'low');
      const any = this.tasks.filter(task => !['high', 'medium', 'low'].includes(task.priority));

      return [...highPriorityTasks, ...mediumPriorityTasks, ...lowPriorityTasks, ...any];
    }
  },
  created() {
    this.tasks = JSON.parse(localStorage.getItem("tasks")) || [];
  },
  methods: {
    toggleTaskStatus(task) {
      task.completed = !task.completed;
      this.saveTasks();
    },
    deleteTask(task) {
      this.tasks = this.tasks.filter((item) => item.id !== task.id);
      this.saveTasks();
    },
    saveTasks() {
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
    updateTasks() {
      this.tasks = JSON.parse(localStorage.getItem("tasks")) || [];
      // console.log("called update");
    },
    editTask(task) {
      const editedTask = window.prompt("Edit task:", task.title);
      if (editedTask !== null && editedTask !== "") {
        task.title = editedTask;
        this.saveTasks();
      }
    },
    changePriority(task) {
      const priority = window.prompt(
        "Set priority (high, medium, low):",
        task.priority
      );
      if (["high", "medium", "low"].includes(priority)) {
        task.priority = priority;
        this.saveTasks();
      }
    },
    
  },
};
</script>

<style scoped>
p {
  font-size: 20px;
  text-align: center;
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
}
#green {
  color: green;
}
h2 {
  font-size: 24px;
  color: orange;
  text-align: center;
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
}
ul {
  width: 700px;
  margin: auto;
}
li {
  display: flex;
  padding: 20px;
  justify-content: space-around;
  margin-bottom: 10px;
  background-color: #ffffff;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}
h1 {
  color: red;
  font-size: 20px;
}
</style>
