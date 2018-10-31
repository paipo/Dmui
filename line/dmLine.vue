<template>
  <div class="tel">
    <span class="title">{{lineTitle}}</span>
    <div class="line" :style="{backgroundColor:lineColor}"></div>
  </div>
</template>

<script>
export default {
  name: 'dmLine',
  data () {
    let lineColor = ''
    if (this.dcolor === undefined) {
      lineColor = '#eeeeee'
    } else {
      lineColor = this.dcolor
    }
    let lineTitle = ''
    if (this.dtitle === undefined) {
      lineTitle = ''
    } else {
      lineTitle = this.dtitle
    }
    return {
      lineColor: lineColor,
      lineTitle: lineTitle
    }
  },
  props: ['dcolor', 'dtitle'],
  methods: {
    borderColor (val) {
      return '#' + this.lineColor
    }
  }
}
</script>

<style scoped>
  .tel{
    height: 30px;
    position: relative;
  }
  .title{
    float: left;
    clear: both;
    color: #cccccc;
    margin-left: 15px;
    margin-bottom: 10px;
  }
  .line{
    width: 100%;
    clear: both;
    height: 1px;
  }
</style>