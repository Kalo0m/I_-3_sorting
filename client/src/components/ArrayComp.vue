<template>
  <div class="container">
  <div class="content">

          <div v-for="(elem, index) in arrayComputed" :key='index' class="arrayElement" v-bind:style="{ height: elem.height +'px', width: '15px', marginLeft: elem.width+'px', backgroundColor: 'rgba(169, 92, 232, 0.8)', color: 'transparent', fontSize: '8px'}">10</div>
      
  </div>
  </div>
</template>

<script>
const config = require('../../config.js');
export default {
  
  name: "ArrayComp",
  props: ["array"],
  data() {
    return {
      width : config.widthArray,
      height : config.heightArray
    };
  },
  computed: {
    arrayComputed: function() {
      const arr = this.array.map((item, index) => {
        return {
          x: index * (config.widthArray / this.array.length),
          y: 0,
          width: config.widthArray / this.array.length - 1,
          height: (item / Math.max(...this.array)) * config.heightArray,
          value: item
        };
      });
      return arr;
    }
  },
};
</script>
<style lang="scss">
@import "../styles.scss";
</style>
