<template>
  <div class="content">
    <v-stage :config="{
      width : this.width,
      height : this.width
    }">
      <v-layer>
        <div v-for="(elem, index) in array" :key='index' class = "oneRect">
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
  }
};
</script>
<style lang="scss">
@import "../styles.scss";
</style>
