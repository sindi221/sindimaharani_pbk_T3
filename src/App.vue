<script setup>
import { reactive } from "vue";
import Header from "./components/header.vue";
import Form from "./components/form.vue";
import List from "./components/list.vue";

const state = reactive({
  tempTask: "",
  filter: "todas",
  tasks: [
    {
      title: "",
      finished: true,
    },

  ],
});

const getTasks = () => {
  return state.tasks.filter((task) => !task.finished);
};

const getTaskFinished = () => {
  return state.tasks.filter((task) => task.finished);
};

const getFilterTasks = () => {
  const { filter } = state;

  switch (filter) {
    case "Undone":
      return getTasks();
    case "Done":
      return getTaskFinished();
    default:
      return state.tasks;
  }
};

const registerTask = () => {
  const newTask = {
    title: state.tempTask,
    finished: false,
  };

  state.tasks.push(newTask);
  state.tempTask = "";
};
</script>

<template>
  <div class="container">
    <Header :get-tasks="getTasks().length" />
    <Form
      :change-filter="(event) => (state.filter = event.target.value)"
      :temp-task="state.tempTask"
      :edit-temp-task="(event) => (state.tempTask = event.target.value)"
      :register-task="registerTask"
    />
    <List :tasks="getFilterTasks()" />
  </div>
</template>

<style>
.container {
  background-image: url('.\assets\tugas.jpeg');
  background-size: cover;
  background-position: center;
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.header {
  text-align: center;
  font-size: 48px; /* Mengubah ukuran font menjadi 48px */
  margin-bottom: 20px;
  font-family: "Arial", sans-serif; /* Mengubah jenis font */
}

.form {
  margin-bottom: 20px;
}

.list {
  width: 100%;
  max-width: 400px;
}

.list-item {
  background-color: white;
  border-radius: 5px;
  padding: 10px;
  margin-bottom: 10px;
  display: flex;
  align-items: center;
}

.task-title {
  flex: 1;
}

.task-status {
  margin-left: 20px;
}

.button {
  cursor: pointer;
  padding: 15px 25px;
  border: none;
  border-radius: 5px;
  background-color: #007bff;
  color: rgba(255, 255, 255, 0.815);
}

.button:hover {
  background-color: #1c5ea5;
}

</style>