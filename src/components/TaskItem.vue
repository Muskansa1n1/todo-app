<template>
  <ul>
    <li>
    <span :class="{ completed: task.completed }">{{ task.title }}</span>    
  </li>
  <div>
       <button @click="toggleStatus">{{ task.completed ? 'Incomplete' : 'Complete' }}</button>
        <button @click="editTask">Edit</button>
        <button @click="deleteTask">Delete</button>
        <button @click="changePriority">Change Priority</button>
  </div>
      <slot></slot>
  </ul>
</template>

<script>
export default {
  props: ['task'],
  methods: {
    toggleStatus() {
      this.$emit('toggleStatus');
    },
    editTask() {
      this.$emit('editTask');
    },
    deleteTask() {
      this.$emit('deleteTask');
    },
    changePriority() {
      this.$emit('changePriority');
    }
  }
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
}
span{
  font-size: 25px;
}
ul{
  width: 700px;

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
div{
  display: flex;
  justify-content: space-around;
  width:400px
}
button {
  padding: 8px 12px;
  background-color: orange;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: orangered;
}
</style>
