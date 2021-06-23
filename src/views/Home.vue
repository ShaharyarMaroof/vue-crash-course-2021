<template>
  <AddTaskForm v-show="showAddTask" @add-task="addTask" />
  <Tasks
    @toggle-reminder="toggleReminder"
    @delete-task="deleteTask"
    :tasks="tasks"
  />
</template>

<script lang="ts">
import Tasks from "../components/Tasks.vue";
import AddTaskForm from "../components/AddTask.vue";

export default {
  name: "Home",
  props: {
    showAddTask: Boolean,
  },
  components: {
    Tasks,
    AddTaskForm,
  },
  data() {
    return {
      tasks: [],
    };
  },
  async created() {
    //@ts-ignore
    this.tasks = await this.fetchTasks();
  },
  methods: {
    async fetchTasks() {
      const response = await fetch("api/tasks");
      const data = await response.json();

      return data;
    },
    async fetchTaskById(id: number) {
      const response = await fetch(`api/tasks/${id}`);
      const data = await response.json();

      return data;
    },
    async addTask(task: any) {
      console.log({ addTask: task });
      const res = await fetch("api/tasks", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(task),
      });
      const newTask = await res.json();
      //@ts-ignore
      this.tasks = [...this.tasks, newTask];
    },
    async deleteTask(id: number) {
      if (confirm("Are you sure?")) {
        const res = await fetch(`api/tasks/${id}`, {
          method: "DELETE",
          headers: {
            "Content-Type": "application/json",
          },
        });

        if (res.status === 200) {
          //@ts-ignore
          this.tasks = this.tasks.filter((task: any) => task.id !== id);
          console.log(`task deleted ${id}`);
        } else {
          alert("There was a problem in deleting this task.");
        }
      }
    },
    async toggleReminder(id: number) {
      const taskToToggle = await this.fetchTaskById(id);
      const updatedTask = { ...taskToToggle, reminder: !taskToToggle.reminder };

      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(updatedTask),
      });

      const data = await res.json();

      //@ts-ignore
      this.tasks = this.tasks.map((task: any) => {
        if (task.id === id) {
          task.reminder = data.reminder;
        }
        return task;
      });
      console.log(`task reminder toggled ${id}`);
    },
  },
};
</script>