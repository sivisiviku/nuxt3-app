<template>
  <nav
    class="bg-gradient-to-r from-emerald-500 to-teal-400 h-max flex justify-between items-center px-8 py-4 shadow-md fixed top-0 left-0 right-0"
  >
    <button
      class="bg-green-300 px-4 py-2 rounded-lg shadow-md text-sm"
      @click="prev"
    >
      &lt;&lt; Previous
    </button>
    <button
      class="bg-green-300 px-4 py-2 rounded-lg shadow-md text-sm"
      @click="open"
    >
      Select Tutorial
    </button>
    <button
      class="bg-green-300 px-4 py-2 rounded-lg shadow-md text-sm"
      @click="next"
    >
      Next >>
    </button>
  </nav>
  <div class="px-8 mt-24">
    <slot />
  </div>
  <TutorialMenu
    v-if="tutorialPopup"
    @emitClose="close"
    @emitTutorial="tutorial($event)"
    :tutorials="tutorials"
  />
  <a
    href="#"
    class="fixed bottom-3 right-3 bg-green-300 p-2 rounded-full shadow-md text-3xl cursor-pointer"
  >
    🔝
  </a>
</template>

<script>
export default {
  data() {
    return {
      tutorialPopup: false,
      currentTutorialNumber: 1,
      tutorials: [
        {
          title: "Baby Name Generator",
          link: "/",
        },
        {
          title: "Tutorial 2",
          link: "/tutorial-2",
        },
        {
          title: "Tutorial 3",
          link: "/tutorial-3",
        },
      ],
    };
  },
  methods: {
    open() {
      this.tutorialPopup = true;
    },
    close() {
      this.tutorialPopup = false;
    },
    prev() {
      if (this.currentTutorialNumber === 1) return;
      else {
        this.currentTutorialNumber = this.currentTutorialNumber - 1;
        if (this.currentTutorialNumber === 1) {
          this.$router.push(`/`);
        } else {
          this.$router.push(`/tutorial-${this.currentTutorialNumber}`);
        }
      }
    },
    next() {
      if (this.currentTutorialNumber === 3) return;
      else {
        this.currentTutorialNumber = this.currentTutorialNumber + 1;
        this.$router.push(`/tutorial-${this.currentTutorialNumber}`);
      }
    },
    tutorial(index) {
      this.currentTutorialNumber = index + 1;
      if (this.currentTutorialNumber === 1) {
        this.$router.push(`/`);
      } else {
        this.$router.push(`/tutorial-${this.currentTutorialNumber}`);
      }
    },
  },
};
</script>

<style scoped></style>
