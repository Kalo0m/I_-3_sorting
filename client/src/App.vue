<template>
  <div id="app">
    <NavBar v-on:lengthChange="changeArrayLength" v-on:algo="algo" />
    <ArrayComp v-bind:array="this.array" />
  </div>
</template>

<script>
import NavBar from "./components/NavBar.vue";
import ArrayComp from "./components/ArrayComp.vue";

export default {
  name: "App",
  data: function() {
    return {
      array: []
    };
  },
  mounted: function() {
    this.array = Array.from({ length: 55 }, () =>
      Math.floor(Math.random() * 100)
    );
  },
  
  methods: {
    changeArrayLength: function(event) {
      this.createRandomArray(event, 100);
    },
    processItem: function(array2, i) {
      return new Promise((resolve) => {
        var index = i;
        for (var j = i + 1; j < array2.length; j++) {
          if (array2[j] < array2[index]) {
            index = j;
          }
        }
        const tmp = array2[index];
        array2[index] = array2[i];
        array2[i] = tmp;
        setTimeout(() => resolve(array2), 1000);
      });
    },

    algo: async function() {
      const array2 = [...this.array];

      console.log("debut algo", { array2 });

      for (var i = 0; i < array2.length; i++) {
        const result = await this.processItem(array2, i);
        console.log(result)
        this.array = result
      }
    } /*
    algo : async function(){
      console.log('debut algo');
      const array2 = [...this.array];
      console.log(array2)

      for(var i =0;i<array2.length;i++){

            var index = i;
            for(var j = i+1;j<array2.length;j++){
              if(array2[j]<array2[index]){
                index = j;
              }
            }
            
            const tmp = array2[index];
            array2[index] = array2[i];
            array2[i] = tmp;
            this.array = array2;
            console.log(this.array)
            await new Promise(resolve => setTimeout(resolve, 100));

      }
      console.log(array2);
    },*/,
    createRandomArray: function(nbElement, max) {
      this.array = Array.from({ length: nbElement }, () =>
        Math.floor(Math.random() * max)
      );
    }
  },

  components: {
    NavBar,
    ArrayComp
  }
};
</script>

<style></style>
