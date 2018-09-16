<template>
  <div class="slider" ref="mySlider">
    <div ref="sd" class="left-btn" :style="{left:valueLeft()}"></div>
    <div class="propo"></div>
    <div class="propo-bg"></div>
    <!-- <div class="right-btn" :class="{active:myPosition.isBtn==1}"></div> -->
    <label v-if="this.value >= 50" style="float:left" class="sd-tip">{{this.value}}</label>
    <label v-if="this.value < 50" style="float:right" class="sd-tip">{{this.value}}</label>
  </div>
</template>
<script type="text/javascript">

export default {
  name: 'dmSlider',
  props: {
    // 当前
    value: {
      type: Number,
      default: 0
    },
    // 默认
    min: {
      type: Number,
      default: 0
    },
    // 默认
    max: {
      type: Number,
      default: 100
    }
  },
  data () {
    console.log('dmSlider data ' + this.value)
    return {
      myPosition: {
        left: 0,
        right: 0,
        now: 0,
        isBtn: 0,
        propoWidth: 0
      },
      myDefault: null,
      ismove: false
    }
  },
  methods: {
    elementLeft (e) { // 计算x坐标
      var offset = e.offsetLeft
      if (e.offsetParent != null) offset += this.elementLeft(e.offsetParent)
      return offset
    },
    elementWidth () { // 计算x坐标
      let e = this.$refs.mySlider
      return e.offsetWidth
    },
    valueLeft () {
      console.log('dmSlider valueLeft ' + this.value)
      return this.value + '%'
    }
  },
  updated () {
    console.log('dmSlider updated ')
  },
  mounted () {
    // 滑块
    let mySlider = this.$refs.mySlider
    let el = this.$refs.sd

    let beginx = this.elementLeft(mySlider)
    let beginw = mySlider.offsetWidth

    console.log('dmSlider mounted ' + this.value)
    // el.style.left = this.value + '%'

    let that = this
    el.onmousedown = function (e) {
      // var disX = e.pageX - el.offsetLeft
      let mySliderX = beginx // 滑动块x坐标
      document.onmousemove = function (e) {
        let pageX = (e.pageX || e.clientX + document.documentElement.scrollLeft) - mySliderX // 获取滑动x坐标
        let cur = parseInt((pageX / beginw) * 100) // 计算百分比
        // let to = e.pageX - disX
        // to = (pageX / mySlider.offsetWidth) * 100 // 计算百分比
        console.log('drag ' + cur)
        if (cur >= 0 && cur <= 100) {
          // el.style.left = cur + '%'
          that.dleft = cur
          // that.valueFun(parseInt(cur))
          that.$emit('input', parseInt(cur))
          // this.$emit('onChangeValue', cur)
        }
      }
      document.onmouseup = function () {
        document.onmousemove = document.onmouseuo = null
      }
      e.preventDefault()
    }
  },
  watch: {
    min (New, old) {
      // this.myDefault()
    },
    max (New, old) {
      // this.myDefault()
    }
  }
}
</script>
<style lang="scss">
    .slider{
            position:relative;
            height: 24px;
            .left-btn,.right-btn{
                position: absolute;
                transform:translate(-50%,0);
                content: "";
                    display: block;
                    height: 24px;
                    width: 14px;
                    background: #999999;
                   border: 1px solid transparent;
                   z-index: 2;
            }
            .propo{
                width: 0%;
                height: 0.04rem;
                background: #999999;
                position: absolute;
                top: 0;
                left: 0;
                z-index: 2;
                display: none;
            }
            .propo-bg{
                background: #cccccc;
                border-radius: 2px;
                height: 2px;
                width:100%;
                position: absolute;
                top: 0;
                left: 0;
                z-index: 1;
                margin-top: 11px;
            }
            .active{
                background: #999999;
            }
    }
    .sd-tip{
      font-size: 11px;
      color:#999999;
      text-align: center;
    }
</style>