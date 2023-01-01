<template>
  <h4
    v-if="title !== undefined && title !== null && title !== ''"
    class="font-bold text-indigo-900 mb-4"
  >
    {{ title }}
  </h4>
  <button
    v-for="(button, index) in buttons"
    :key="index"
    class="bg-white text-indigo-900 font-semibold border-t-2 border-l-2 border-b-2 border-orange-600 py-1 px-8 hover:bg-orange-600 hover:text-white focus:bg-orange-600 focus:text-white"
    :class="{
      'border-r-2': index + 1 === buttons.length,
      'rounded-l-xl': index === 0,
      'rounded-r-xl': index + 1 === buttons.length,
      'bg-orange-600': selectedIndex === index,
      'text-white': selectedIndex === index,
    }"
    @click="$emit('emitClick', index)"
  >
    {{ button }}
  </button>
</template>

<script setup>
const props = defineProps(["title", "buttons", "selectedIndex"]);
</script>

<style lang="scss" scoped></style>
