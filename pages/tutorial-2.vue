<template>
  <div class="bg-slate-700 h-full fixed top-0 left-0 right-0 -z-10"></div>
  <main class="text-center">
    <h1 class="text-white text-5xl font-bold">Task Board</h1>
    <p class="text-white mt-2 text-xl">Create a list of tasks</p>

    <div class="mt-10">
      <input
        class="bg-transparent border-b-2 border-white outline-none text-white text-2xl"
        type="text"
        v-model="newTask"
        placeholder="Add a new task"
        @keypress.enter="addTask"
      />
      <button
        class="px-4 py-2 bg-green-400 rounded-xl text-2xl font-bold ml-4"
        @click="addTask"
      >
        ADD
      </button>
    </div>

    <div class="mt-10">
      <Task
        v-for="(task, i) in tasks"
        :key="i"
        :task="task"
        :index="i"
        @toggleDone="toggleDone"
        @deleteTask="deleteTask"
      />
    </div>
  </main>
</template>

<script>
import { tasks } from "@/data/tasks";

export default {
  data() {
    return {
      newTask: "",
      tasks: [],
    };
  },
  methods: {
    addTask() {
      if (this.newTask) {
        tasks.data.push({ content: this.newTask, done: false });
        this.tasks = tasks.data;
        this.newTask = "";
      }
    },
    toggleDone(index) {
      this.tasks[index].done = !this.tasks[index].done;
      tasks.data = this.tasks;
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
      tasks.data = this.tasks;
    },
  },
  created() {
    this.tasks = tasks.data;
  },
};
</script>

<style lang="scss" scoped></style>
