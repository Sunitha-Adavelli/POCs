<template>
  <div class="todo-list">
    <h1>ToDo List</h1>
    <input v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task" />
    <ul>
      <li v-for="(task, index) in filteredTasks" :key="index">
        <input type="checkbox" v-model="task.completed" />
        <span :class="{ completed: task.completed }">{{ task.text }}</span>
        <button @click="deleteTask(index)">Delete</button>
      </li>
    </ul>
    <div class="filters">
      <button @click="filter = 'all'">All</button>
      <button @click="filter = 'active'">Active</button>
      <button @click="filter = 'completed'">Completed</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [],
      filter: 'all'
    };
  },
  computed: {
    filteredTasks() {
      if (this.filter === 'active') {
        return this.tasks.filter(task => !task.completed);
      } else if (this.filter === 'completed') {
        return this.tasks.filter(task => task.completed);
      }
      return this.tasks;
    }
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({ text: this.newTask, completed: false });
        this.newTask = '';
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    }
  }
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
}
.filters button {
  margin-right: 10px;
}
</style>
