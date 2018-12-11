<template>
  <div class="clocks">
      <canvas :id="uid" :width="clockRadius" :height="clockRadius" ></canvas>
  </div>
</template>

<script>
export default {
  name: 'dmClock',
  data () {
    return {
      timeAuto999: null,
      uid: Number(Math.random().toString().substr(3, length) + Date.now()).toString(36),
      canvas: null,
      ctx: null,
      stop: false,
      clockImage: new Image()
    }
  },
  mounted () {
    this.dateBegin()
  },
  props: ['dauto', 'dvalue', 'dstop', 'clockRadius', 'colorscale', 'colorhour', 'colorminute', 'colorsecond'],
  methods: {
    w () {
      return this.clockRadius + 'px'
    },
    // draw functions :
    clear () { // clear canvas function
      this.ctx.clearRect(0, 0, this.ctx.canvas.width, this.ctx.canvas.height)
    },
    drawScene () {
      this.clear() // clear canvas

      // console.log('drawScene ' + this.clockRadius)

      // get current time
      var date = new Date()
      var hours = date.getHours()
      var minutes = date.getMinutes()
      var seconds = date.getSeconds()
      hours = hours > 12 ? hours - 12 : hours
      var hour = hours + minutes / 60
      var minute = minutes + seconds / 60

      // save current context
      this.ctx.save()

      // draw clock image (as background)
      this.ctx.drawImage(this.clockImage, 0, 0, 500, 500)

      this.ctx.translate(this.canvas.width / 2, this.canvas.height / 2)
      this.ctx.beginPath()

      // draw numbers
      this.ctx.font = '14px Arial'
      this.ctx.fillStyle = this.colorscale
      this.ctx.textAlign = 'center'
      this.ctx.textBaseline = 'middle'
      for (var n = 1; n <= 12; n++) {
        var theta = (n - 3) * (Math.PI * 2) / 12
        var x = this.clockRadius * 0.4 * Math.cos(theta)
        var y = this.clockRadius * 0.4 * Math.sin(theta)
        this.ctx.fillText(n, x, y)
      }

      this.ctx.fillStyle = this.colorhour
      // draw hour
      this.ctx.save()
      theta = (hour - 3) * 2 * Math.PI / 12
      this.ctx.rotate(theta)
      this.ctx.beginPath()
      this.ctx.moveTo(-15, -2)
      this.ctx.lineTo(-15, 2)
      this.ctx.lineTo(this.clockRadius * 0.2, 1)
      this.ctx.lineTo(this.clockRadius * 0.2, -1)
      this.ctx.fill()
      this.ctx.restore()

      this.ctx.fillStyle = this.colorminute
      // draw minute
      this.ctx.save()
      theta = (minute - 15) * 2 * Math.PI / 60
      this.ctx.rotate(theta)
      this.ctx.beginPath()
      this.ctx.moveTo(-15, -2)
      this.ctx.lineTo(-15, 2)
      this.ctx.lineTo(this.clockRadius * 0.4, 1)
      this.ctx.lineTo(this.clockRadius * 0.4, -1)
      this.ctx.fill()
      this.ctx.restore()

      this.ctx.fillStyle = this.colorsecond
      // draw second
      this.ctx.save()
      theta = (seconds - 15) * 2 * Math.PI / 60
      this.ctx.rotate(theta)
      this.ctx.beginPath()
      this.ctx.moveTo(-15, -1)
      this.ctx.lineTo(-15, 1)
      this.ctx.lineTo(this.clockRadius * 0.4, 0)
      this.ctx.lineTo(this.clockRadius * 0.4, 0)
      this.ctx.fill()
      this.ctx.restore()

      this.ctx.restore()
    },
    printDate () {
      this.value = this.frontOneHour(this.format)
    },
    dateStop () {
      this.stop = true
    },
    dateBegin () {
      // initialization
      this.canvas = document.getElementById(this.uid)
      this.ctx = this.canvas.getContext('2d')

      // var width = canvas.width;
      // var height = canvas.height;

      this.clockImage = new Image()
      this.clockImage.src = ''

      this.drawScene()
      if (this.timeAuto999 === null) {
        this.timeAuto999 = setInterval(this.drawScene, 1000) // loop drawScene
      }
    }
  }
}
</script>

<style scoped>
  .clocks {
    
  }
</style>