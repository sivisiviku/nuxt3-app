<template>
  <div
    class="flex justify-between items-center bg-slate-500 p-4 mb-4 rounded-lg"
  >
    <div
      class="text-white text-xl"
      :class="{ 'line-through': task.done === true }"
    >
      {{ task.content }}
    </div>
    <div>
      <button
        class="bg-green-400 rounded-xl px-4 py-2 font-bold"
        @click="toggleDone(index)"
      >
        {{ task.done === false ? "Done" : "Undo" }}
      </button>
      <button
        class="bg-red-400 rounded-xl px-4 py-2 font-bold ml-3"
        @click="deleteTask(index)"
      >
        Delete
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["task", "index"],
  methods: {
    toggleDone(index) {
      this.$emit("toggleDone", index);
    },
    deleteTask(index) {
      this.$emit("deleteTask", index);
    },
  },
};
</script>

<style lang="scss" scoped></style>
