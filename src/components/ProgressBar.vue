<template>
  <div id="main">
    <div class="title">
      {{title}}
    </div>
    <div class="bar_container">
      <div class="progress">
        <div :class="`progress_bar percent-${Math.round(100 / total * progress)}`">
          {{percent}}
        </div>
        <div class="progress_bar_shadow percent-100">
          
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProgressBar',
  props: {
    progress : {
      type : Number
    },
    total: {
      type : Number
    },
    title: {
      type : String
    }
  },
  computed: {
    percent : function() { return `${Math.round(100 / this.total * this.progress)}%` }
  },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="sass">
@use "sass:math"

#main
  width: 100%
.title
  font-size: 20px
  color: white
  text-align: center
  font-family: Arial
  padding: 10px

.bar_container
  width: 100%
  height: 40px
  background-color: white
  position: relative
  padding: 0 5px
  .progress_bar,.progress_bar_shadow
    position: absolute
    height: 30px
    z-index: 2
    top: 5px
  .progress_bar_shadow
    z-index: 1
    background-color: #dfdfdf
  .progress_bar
    text-align: center
    font-size: 25px
    color: white
    font-family: Arial
    min-width: 40px
    transition: 500ms
    background: linear-gradient(.25turn,rgb(0,65,255),rgba(255,0,0))
@for $col from 0 through 100
  .percent-#{$col}
    width: calc( #{percentage(math.div($col,100))} - 10px)
</style>
