<template>
  <div class="tel">
    <div>{{value}}</div>
  </div>
</template>

<script>
export default {
  name: 'dmDate',
  data () {
    let data = {
      timeAuto998: null,
      auto: false,
      value: '...',
      stop: false,
      format: 'yyyy-MM-dd hh:mm:ss'
    }
    if (this.dauto !== undefined) {
      data.auto = this.dauto
    }
    if (this.dvalue !== undefined) {
      data.value = this.dvalue
    }
    if (this.dstop !== undefined) {
      data.stop = this.dstop
    }
    if (this.dformat !== undefined) {
      data.format = this.dformat
    }
    return {
      auto: data.auto,
      value: data.value,
      stop: data.stop,
      format: data.format
    }
  },
  mounted () {
    this.dateBegin()
  },
  props: ['dauto', 'dvalue', 'dstop', 'dformat'],
  methods: {
    printDate () {
      this.value = this.frontOneHour(this.format)
    },
    dateStop () {
      this.stop = true
    },
    dateBegin () {
      if (this.timeAuto998 !== null) {
        clearTimeout(this.timeAuto998)
      }
      this.printDate()
      let that = this
      this.timeAuto998 = setInterval(function () {
        that.printDate()
      }, 1000)
    },
    frontOneHour (fmt) {
      if (this.stop === true) {
        if (this.timeAuto998 !== null) {
          clearTimeout(this.timeAuto998)
        }
      }
      var currentTime = new Date(new Date().getTime())
      // console.log(currentTime) // Wed Jun 20 2018 16:12:12 GMT+0800 (中国标准时间)
      var o = {
        'M+': currentTime.getMonth() + 1, // 月份
        'd+': currentTime.getDate(), // 日
        'h+': currentTime.getHours(), // 小时
        'm+': currentTime.getMinutes(), // 分
        's+': currentTime.getSeconds(), // 秒
        'q+': Math.floor((currentTime.getMonth() + 3) / 3), // 季度
        'S': currentTime.getMilliseconds() // 毫秒
      }
      if (/(y+)/.test(fmt)) fmt = fmt.replace(RegExp.$1, (currentTime.getFullYear() + '').substr(4 - RegExp.$1.length))
      for (var k in o) {
        if (new RegExp('(' + k + ')').test(fmt)) fmt = fmt.replace(RegExp.$1, (RegExp.$1.length === 1) ? (o[k]) : (('00' + o[k]).substr(('' + o[k]).length)))
      }
      return fmt
    }
  }
}
</script>

<style scoped>
  .tel{
  }
</style>