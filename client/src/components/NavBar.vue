<template>
  <div>
    <nav class='navbar'> <p>Taille du tableau : </p><input v-model='taille' @input="lengthChange" type="range" id="volume" name="volume"
         min="10" max="100" value="55"><a @click='lengthChange' class='reset-array'>Changer les valeurs</a><a class='reset-array' @click='algo'>Algo 1</a></nav>
  </div>
</template>

<script>
export default {
  name: 'NavBar',
  data: function(){
    return {
      taille : 55
    } 
  },
  methods: {
    lengthChange : function(){
      this.$emit('lengthChange',this.taille)
    },
    algo: function(){
      this.$emit('algo')
    }
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
  @import '../styles.scss';
</style>
