<template>
    <div class="todo">
      <h1 class="green">My Todo List</h1>
      <form @submit.prevent="addTask">
        <input type="text" v-model="newTask" placeholder="Add a new task" />
        <button type="submit">Add Task</button>
      </form>
      <ul>
        <li v-for="(task, index) in tasks" :key="index">
          <input type="checkbox" v-model="task.completed" @change="updateTask(index)" />
          <span :class="{ completed: task.completed }">{{ task.title }}</span>
          <button @click="removeTask(index)">Remove</button>
          <button @click="editTask(index)">Edit</button>
        </li>
      </ul>
      <div v-if="editIndex !== null">
        <h2>Edit Task</h2>
        <form @submit.prevent="updateTaskText">
          <input type="text" v-model="editedTaskText" placeholder="Enter task text" />
          <button type="submit">Update Task</button>
          <button type="button" @click="cancelEdit">Cancel</button>
        </form>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        newTask: "",
        tasks: [],
        editIndex: null,
        editedTaskText: ""
      };
    },
    created() {
      this.loadTasks();
    },
    methods: {
      addTask() {
        if (this.newTask.trim() === "") return;
        this.tasks.push({
          title: this.newTask,
          completed: false
        });
        this.newTask = "";
        this.saveTasks();
      },
      updateTask(index) {
        this.saveTasks();
      },
      removeTask(index) {
        this.tasks.splice(index, 1);
        this.saveTasks();
      },
      editTask(index) {
        this.editIndex = index;
        this.editedTaskText = this.tasks[index].title;
      },
      updateTaskText() {
        if (this.editedTaskText.trim() === "") {
          this.cancelEdit();
          return;
        }
        this.tasks[this.editIndex].title = this.editedTaskText;
        this.saveTasks();
        this.cancelEdit();
      },
      cancelEdit() {
        this.editIndex = null;
        this.editedTaskText = "";
      },
      saveTasks() {
        localStorage.setItem("tasks", JSON.stringify(this.tasks));
      },
      loadTasks() {
        const tasks = localStorage.getItem("tasks");
        if (tasks) {
          this.tasks = JSON.parse(tasks);
        }
      }
    }
  };
  </script>
  
  <style>
.todo {
  font-family: Arial, sans-serif;
  max-width: 600px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

.todo h1 {
  font-size: 2em;
  text-align: center;
}

.todo form {
  margin-bottom: 20px;
}

.todo input[type="text"] {
  font-size: 1.2em;
  padding: 10px;
  border: none;
  border-radius: 8px;
  box-shadow: 0 0 4px rgba(88, 47, 47, 0.1);
  margin-right: 10px;
  width: 60%;
  display: inline-block;
  background: none;
  border:1px solid #383838;
}

.todo button {
  font-size: 1.2em;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  background-color: #007bff;
  cursor: pointer;
}

.todo button:hover {
  background-color: #0069d9;
}

.todo ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.todo li {
  margin-bottom: 10px;
  display: flex;
  align-items: center;
}

.todo li input[type="checkbox"] {
  margin-right: 10px;
}

.todo li span.completed {
  text-decoration: line-through;
}

.todo li input[type="text"] {
  font-size: 1.2em;
  padding: 10px;
  border: none;
  border-radius: 4px;
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.1);
  width: 60%;
}

.todo li button {
  font-size: 1em;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  background-color: #ffc107;
  color: white;
  cursor: pointer;
  margin-left: 10px;
}

.todo li button:hover {
  background-color: #e0a800;
}

.todo li button:first-of-type {
  background-color: #dc3545;
  color: black;
}

.todo li button:first-of-type:hover {
  background-color: #c82333;
}
</style>
