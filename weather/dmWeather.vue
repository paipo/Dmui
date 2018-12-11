<template class="tel">
<div class="one1">
  <div class="one2">
    <div class="wht_lg"></div>
    <div class="wht_c"><span :style="{fontSize:dqtSize(),fontFamily:fam()}">{{c}}</span><span :style="{fontSize:dqcSize(),fontFamily:fam()}">{{cc}}</span></div>
    <div class="wht_tip" :style="{fontSize:dqsSize(),fontFamily:fam()}">{{tip}}</div>
    <div class="wht_dq">
      <span class="dq1" :style="{fontSize:dq1Size(),fontFamily:fam()}">{{d1}}</span>
      <span class="dq2" :style="{fontSize:dq2Size(),fontFamily:fam()}">{{d2}}</span>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'dmWeather',
  data () {
    let d1 = ''
    if (this.dq1) {
      d1 = this.dq1
    } else {
      d1 = '成都'
    }
    let d2 = ''
    if (this.dq2) {
      d2 = this.dq2
    } else {
      d2 = '四川'
    }
    return {
      c: '17',
      cc: '℃',
      tip: '太阳',
      d1: d1,
      d2: d2,
      isShow: false
    }
  },
  props: ['title', 'dq1', 'dq2', 'type', 'fontsize', 'famili'],
  computed: {
  },
  methods: {
    fam () {
      if (this.famili) {
        return this.famili
      }
      return '黑体'
    },
    dqtSize () {
      if (this.fontsize) {
        return this.fontsize + 'px'
      }
      return '47px'
    },
    dqcSize () {
      if (this.fontsize) {
        return (this.fontsize - 20) + 'px'
      }
      return '27px'
    },
    dqsSize () {
      if (this.fontsize) {
        return (this.fontsize - 20) + 'px'
      }
      return '27px'
    },
    dq1Size () {
      if (this.fontsize) {
        return (this.fontsize - 20) + 'px'
      }
      return '27px'
    },
    dq2Size () {
      if (this.fontsize) {
        return (this.fontsize - 30) + 'px'
      }
      return '17px'
    }
  }
}
</script>

<style scoped>
.tel{
  height: 100%;
}
  .one1 {
    height:100%;
    width:100%;
    display: flex;
    justify-content:center;
    align-items:center;
  }
  .one2 {
    display: table;
  }
  .wht_c {
    clear: both;
    text-align: center; 
    width: 100%;
  }
  .wht_dq {
    clear: both;
    text-align: center;
    margin-top:10px;
    width: 100%;
  }
  .wht_tip {
    clear: both;
    text-align: center; 
    width: 100%;
    margin-top:10px;
  }
  .wht_lg{
    clear: both;
    text-align: center; 
    width: 100%;
  }
.dsum-lr {
  height:100%;
  width:100%;
  display: flex;
  justify-content:center;
  align-items:center;
}

.dsum-title-b{
  clear: both;
  text-align: center; 
}
.dsum-value-b{
  clear: both;
  text-align: center; 
  position: relative;
  top:10px;
}
</style>
