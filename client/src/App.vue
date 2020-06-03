<template>
  <div id="app">
    <NavBar v-on:lengthChange='changeArrayLength'  v-on:algo='algo' />
    <ArrayComp v-bind:array="arrayComputed" />
  </div>
</template>

<script>
import NavBar from "./components/NavBar.vue";
import ArrayComp from "./components/ArrayComp.vue";
const config = require('../config.js');

export default {
  name: "App",
  data: function() {
    return {
      array: []
    };
  },
  mounted : function(){
    this.array = Array.from({length: 55}, () => Math.floor(Math.random() * 100));
  },
  computed : {
    arrayComputed : function(){
      const arr = this.array.map((item, index) => {
        return{
          x : index*(config.widthArray/this.array.length),
          y : 0,
          width : config.widthArray/this.array.length-2,
          height : (item/Math.max(...this.array))*config.heightArray,
          value : item
        }
      });
     

      return arr;
    }
  },
  methods: {
    changeArrayLength: function(event){
      this.createRandomArray(event,100)

    },
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
    },
    createRandomArray: function(nbElement,max) {
      this.array = Array.from({length: nbElement}, () => Math.floor(Math.random() * max));
    }
  },
  
  components: {
    NavBar,
    ArrayComp
  }
};
</script>

<style></style>
