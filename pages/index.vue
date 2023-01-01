<template>
  <h1 class="text-4xl font-bold text-indigo-900 text-center mb-8">
    Baby Name Generator
  </h1>
  <p class="text-indigo-900 text-center mb-16">
    Choose your options and click the "Find Names" button below
  </p>
  <div class="bg-red-100 rounded-3xl py-8 text-center mb-8">
    <div v-for="(optionCategory, index) in optionCategories" :key="index">
      <ButtonGroup
        :title="optionCategory.title"
        :buttons="optionCategory.buttons"
        :selectedIndex="
          optionCategory.buttons.indexOf(options[`${optionCategory.name}`])
        "
        @emitClick="
          (index) =>
            (options[`${optionCategory.name}`] = optionCategory.buttons[index])
        "
      />
      <br /><br />
    </div>
    <br />
    <button
      class="bg-orange-600 text-white font-semibold rounded-full py-2 px-16 hover:bg-orange-700"
      @click="computeSelectedNames"
    >
      Find Names
    </button>
  </div>
  <div class="flex justify-center">
    <div
      class="bg-white text-indigo-900 text-xl font-bold w-max border-2 border-orange-600 rounded-xl pt-4 pb-2 pr-10 pl-6 mx-2 relative"
      v-for="(selectedName, index) in selectedNames"
      :key="index"
    >
      {{ selectedName }}
      <span
        class="absolute -top-0 right-0 text-xl cursor-pointer"
        @click="selectedNames.splice(index, 1)"
        >❎</span
      >
    </div>
  </div>
</template>

<script setup>
import { names } from "@/data/names";

const optionCategories = [
  {
    name: "gender",
    title: "1) Choose a gender",
    buttons: ["Boy", "Unisex", "Girl"],
  },
  {
    name: "popularity",
    title: "2) Choose the name's popularity",
    buttons: ["Trendy", "Unique"],
  },
  {
    name: "length",
    title: "3) Choose the name's length",
    buttons: ["Long", "All", "Short"],
  },
];
const options = reactive({
  gender: "Girl",
  popularity: "Unique",
  length: "Short",
});
const selectedNames = ref([]);
function computeSelectedNames() {
  const filterLevel1 = names.gender[`${options.gender.toLowerCase()}`];
  const filterLevel2 = names.popularity[
    `${options.popularity.toLowerCase()}`
  ].filter((val) => filterLevel1.includes(val));
  const filterLevel3 = names.length[`${options.length.toLowerCase()}`].filter(
    (val) => filterLevel2.includes(val)
  );
  selectedNames.value = filterLevel3;
}
</script>

<style lang="scss" scoped></style>
