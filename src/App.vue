<template>
  <div>
    <task-form @addTask="addTask"></task-form>
    <task-list ref="taskList" :tasks="tasks"></task-list>
  </div>
</template>

<script>
import TaskForm from "./components/TaskForm.vue";
import TaskList from "./components/TaskList.vue";

export default {
  components: {
    TaskForm,
    TaskList,
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    addTask(task) {
      this.tasks = JSON.parse(localStorage.getItem("tasks")) || [];
      this.tasks.push(task);
      this.saveTasks();
    },
    saveTasks() {
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
      this.$refs.taskList.updateTasks();
    },
  },
  mounted() {
    this.tasks = JSON.parse(localStorage.getItem("tasks")) || [];
  },
};
</script>
