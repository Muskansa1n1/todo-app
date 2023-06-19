<template>
  <div>
    <h2>Add Task</h2>
    <form @submit.prevent="addTask">
      <input type="text" v-model="taskTitle" placeholder="Enter the task" required>
      <button type="submit">Add Task</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      taskTitle: ''
    };
  },
  methods: {
    addTask() {
      if (this.taskTitle !== '') {
        this.$emit('addTask', {
          id: Date.now(),
          title: this.taskTitle,
          completed: false
        });
        this.taskTitle = '';
      }
    }
  }
};
</script>
<style scoped>
form {
  margin: 20px auto;
  max-width: 400px;
  background-color: #f8f8f8;
  border-radius: 8px;
  padding: 20px;
}
h2 {
  font-size: 24px;
  color: orange;
  text-align: center;
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}

form {
  display: flex;
}

form input[type="text"] {
  flex-grow: 1;
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

form button {
  margin-left: 10px;
  padding: 5px 10px;
  border: none;
  background-color: orange;
  color: #fff;
  cursor: pointer;
  border-radius: 4px;
}

form button:hover {
  background-color: orangered;
}

form button:focus {
  outline: none;
}
</style>
