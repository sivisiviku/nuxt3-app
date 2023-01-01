<template>
  <div
    class="bg-black fixed top-0 left-0 bottom-0 right-0 z-10 bg-opacity-30 flex justify-center items-center"
  >
    <div
      class="w-1/2 h-1/2 bg-gradient-to-br from-green-100 to-emerald-200 rounded-xl pt-12 pb-8 px-10 relative"
    >
      <button class="text-2xl absolute top-1 right-1" @click="emitClose">
        ❎
      </button>
      <div class="h-full overflow-auto no-scrollbar">
        <div
          v-for="(tutorial, index) in tutorials"
          :key="index"
          class="bg-green-300 px-4 py-2 rounded-lg shadow-md text-sm mb-3 cursor-pointer"
          @click="emitTutorial(index)"
        >
          {{ tutorial.title }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["tutorials"],
  methods: {
    emitClose() {
      this.$emit("emitClose");
    },
    emitTutorial(index) {
      this.$emit("emitTutorial", index);
    },
  },
};
</script>

<style scoped></style>
