<script setup>
  import { ref } from 'vue';
  
  const taskId = ref(0);
  const taskName = ref('');
  const taskNameError = ref(false);
  const taskList = ref([]);
  const taskCompleted = ref(false);
  
  function addTask() {
    if (taskName.value.trim() !== '') {
      taskList.value.push({
        id: taskId.value++,
        name: taskName.value,
        completed: taskCompleted.value
      });
      taskName.value = '';
      taskNameError.value = false; 
    } else {
      taskNameError.value = true; 
    }
  }
  
  function removeTask(task) {
    const index = taskList.value.indexOf(task);
    if (index !== -1) {
      taskList.value.splice(index, 1);
    }
  }
  </script>

<template>
    <div>
      <h1>My ToDo List</h1>
      <input
        type="text"
        v-model="taskName"
        @keydown.enter="addTask"
        :style="{ border: taskNameError ? '2px solid red' : '1px solid #ccc' }"
        placeholder="Enter a task..."
      >
      <span v-if="taskNameError" class="error-message">Please enter a task</span>
      <button class="buttonstyle" @click="addTask">Add Task</button>
      <transition-group name="task-fade">
        <li
          v-for="(task, index) in taskList"
          :key="task.id"
          :class="{
            'task-item': true,
            'entering-red': !task.completed,
            'entering-green': task.completed
          }"
        >
          <div class="task-content">
            <input type="checkbox" v-model="task.completed">
            <span :class="{ done: task.completed }">{{ index + 1 }}. {{ task.name }}</span>
          </div>
          <button @click="removeTask(task)">Remove</button>
        </li>
      </transition-group>
    </div>
  </template>
  
  <style scoped>

/* Error message style */
.error-message {
  color: red;
  font-size: 12px;
  display: block;
  margin-top: 5px;
}

/* Animation styles */
/* Fade animation for entering and leaving */
.task-fade-enter-active,
.task-fade-leave-active {
  transition: opacity 0.5s, transform 0.5s;
}
.task-fade-enter,
.task-fade-leave-to {
  opacity: 0;
  transform: translateX(100%); /* Slide to the right during removal */
}

/* Task item container */
.task-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  width: 100%; 
}

/* Task background color variations */
.entering-red {
  background-color: palevioletred; /* Initial background color */
}

.entering-green {
  background-color: palegreen; /* Background color when task is completed */
}

/* Completed task text style */
.done {
  text-decoration: line-through; 
}

/* Input text box style */
input[type="text"] {
  width: 100%; 
  padding: 10px;
  font-size: 20px;
}

/* Checkbox style */
input[type="checkbox"] {
  font-size: 20px;
  margin-right: 1px;
}

/* Add task button style */
.buttonstyle {
  width: 100%; 
  background-color: #446fe6;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

/* Task list container style */
div {
  border-radius: 5px;
  background-color: #f2f2f2d4;
  padding: 20px;
}

/* Heading style */
h1 {
  width: 100%;
  text-align: center;
}

/* Task content style */
.task-content {
  display: flex;
  align-items: center;
}

/* Task description style */
span {
  padding-left: 10px;
  font-size: 20px;
}

</style>
