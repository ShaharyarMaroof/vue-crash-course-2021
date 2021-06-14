<template>
  <div class="container">
    <Header title="Task Tracker" />
    <AddTaskForm @add-task="addTask" />
    <Tasks
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask"
      :tasks="tasks"
    />
  </div>
</template>

<script lang="ts">
import Header from "./components/Header.vue";
import Tasks from "./components/Tasks.vue";
import AddTaskForm from "./components/AddTask.vue";

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTaskForm,
  },
  data() {
    return {
      tasks: [],
    };
  },
  created() {
    //@ts-ignore
    this.tasks = [
      {
        id: 1,
        text: "test task",
        reminder: true,
        day: "June 14, 2021 at 03:30pm",
      },
    ];
  },
  methods: {
    addTask(task: any) {
      //@ts-ignore
      this.tasks = [...this.tasks, task];
    },
    deleteTask(id: number) {
      if (confirm("Are you sure?")) {
        //@ts-ignore
        this.tasks = this.tasks.filter((task: any) => task.id !== id);
        console.log(`task deleted ${id}`);
      }
    },
    toggleReminder(id: number) {
      //@ts-ignore
      this.tasks = this.tasks.map((task: any) => {
        if (task.id === id) {
          task.reminder = !task.reminder;
        }
        return task;
      });
      console.log(`task reminder toggled ${id}`);
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: "Poppins", sans-serif;
}

.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;

  &:focus {
    outline: none;
  }
  &:active {
    transform: scale(0.98);
  }
}

.btn-block {
  display: block;
  width: 100%;
}
</style>
