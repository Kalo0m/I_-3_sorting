<template>
  <div class="content">
    <v-stage :config="{
      width : this.width,
      height : this.width
    }">
      <v-layer>
        <div v-for="(elem, index) in arrayComputed" :key='index' class = "oneRect">
        <v-rect  :config="{
          x: elem.x,
          y: elem.y,
          width: elem.width,
          height: elem.height,
          fill: 'grey',
        }"
      /></div>
      </v-layer>
    </v-stage>
    
    {{array}}
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
          width: config.widthArray / this.array.length - 2,
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
