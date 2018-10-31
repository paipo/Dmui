<template>
  <div class="tel">
   <div class='dsum'>
      <div class='dsum-title' :style='fontc'>{{dtitle}}</div>
      <div class='dsum-value' :style='fontb'>{{dvalue}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'dmSum',
  data () {
    return {
      title: this.dtitle,
      value: this.dvalue
    }
  },
  props: ['dtitle', 'dvalue', 'fontc', 'fontb'],
  mounted () {
  },
  methods: {
  }
}
</script>

<style scoped>
.dsum {
  height:100%;
  width:100%;
}
.dsum-title{
  float:left;
}
.dsum-value{
  clear: both;
  float:left;
  margin-left: 10px;
  margin-top: 10px;
}
  .tel{
    height: 30px;
    position: relative;
  }
  .title{
    float: left;
    clear: both;
  }
  .line{
    width: 100%;
    clear: both;
  }
  .line td{
    padding: 5px 0px;
  }
  .line:hover{
  }
  .dmti_value{
    height: 30px;
    border: none;
    border-bottom: solid 1px #eeeeee;
    width: 70px;
    text-align: center;
    margin-left: 10px;
  }
  .dmti_heard{
    height: 30px;
    border: none;
    border-bottom: solid 1px #eeeeee;
    width: 60px;
    text-align: center;
  }
  .btndel{
    position: relative;
    right: 5px;
    margin-top: 0px;
    margin-left: 15px;
  }
  .heard{
    background-color: #eeeeee;
    height: 45px;
    line-height: 45px;
  }
</style>