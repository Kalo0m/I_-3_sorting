<template>
  <div id="app">
    <NavBar @lengthChange="generateRandomArray" @algo="algo" />
    <ArrayComp :array="array" />
  </div>
</template>

<script>
import NavBar from "./components/NavBar.vue";
import ArrayComp from "./components/ArrayComp.vue";

export default {
  name: "App",

  data() {
    return {
      array: [],
      running: false
    };
  },

  mounted() {
    this.generateRandomArray(55);
  },

  methods: {
    createRandomArray(length, max = 100) {
      return Array.from({ length }, () => Math.floor(Math.random() * max));
    },

    generateRandomArray(length) {
      this.array = this.createRandomArray(length)
    },

    processItems(items, i) {
      if (items.length - 1 === i) {
        console.log("End running...");
        return this.running = false;
      }

      let index = i;

      for (let j = i + 1; j < items.length; j++) {
        if (items[j] < items[index]) {
          index = j;
        }
      }

      const tmp = items[index];
      items[index] = items[i];
      items[i] = tmp;

      this.array = [...items];

      setTimeout(() => this.processItems(items, i + 1), 100);
    },

    algo() {
      if (this.running) {
        return console.warn('Already running...');
      }

      this.running = true;
      console.log("Start running...");
      this.processItems(this.array, 0);
    },
  },

  components: {
    NavBar,
    ArrayComp
  }
};
</script>

<style></style>
