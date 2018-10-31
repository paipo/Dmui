<template>
 <div class="mouseselect" :style={display:display,width:swidth(),height:sheight(),left:sleft(),top:stop(),border:sborder()}></div>
</template>

<script>
var dmMouseSelectDown = null
export default {
  name: 'dmMouseSelect',
  data () {
    return {
      display: 'none',
      width: 0,
      height: 0,
      left: 0,
      top: 0,
      startX: 0,
      startY: 0,
      lastMouseX: 0,
      lastMouseY: 0,
      handle: false
    }
  },
  props: [
    'border',
    'borderWidth',
    'borderColor',
    'body',
    'itop'
  ],
  computed: {
  },
  methods: {
    sborder () {
      if (this.border === '') {
        return 'solid 1px #000000'
      }
      return this.border
    },
    swidth () {
      return this.width + 'px'
    },
    sheight () {
      return this.height + 'px'
    },
    sleft () {
      return this.left + 'px'
    },
    stop () {
      if (this.itop !== undefined) {
        return (this.top - this.itop) + 'px'
      } else {
        return (this.top) + 'px'
      }
    },
    start () {
      console.log('dmmouseselect start')
      // document.addEventListener('touchend touchcancel', this.handleBegin, true)
      if (this.body === '') {
        document.addEventListener('mousedown', this.handleDown, true)
        document.addEventListener('mousemove', this.handleMove, true)
        document.addEventListener('mouseup', this.handleUp, true)
      } else {
        document.getElementById(this.body).addEventListener('mousedown', this.handleDown, true)
        document.getElementById(this.body).addEventListener('mousemove', this.handleMove, true)
        document.getElementById(this.body).addEventListener('mouseup', this.handleUp, true)
      }
    },
    handleDown (e) {
      console.log('dmmouseselect handleDown')
      let that = this
      this.startX = e.pageX || e.clientX + document.documentElement.scrollLeft
      this.startY = e.pageY || e.clientY + document.documentElement.scrollTop
      dmMouseSelectDown = setTimeout(function () {
        that.handleBegin(e)
      }, 200)
      this.$emit('selectDown', e, this.startX, this.startY)
      // if (e.stopPropagation) e.stopPropagation()
      // if (e.preventDefault) e.preventDefault()
    },
    handleBegin (e) {
      console.log('dmmouseselect hadleBegin')
      console.log(e.pageX || e.clientX + document.documentElement.scrollLeft)
      // let _x = e.pageX || e.clientX + document.documentElement.scrollLeft
      // let _y = e.pageY || e.clientY + document.documentElement.scrollTop
      // if (_x !== this.startX || _y !== this.startY) {
      //   console.log('dmmouseselect hadleBegin back')
      //   return
      // }
      this.handle = true
      // this.startX = e.pageX || e.clientX + document.documentElement.scrollLeft
      // this.startY = e.pageY || e.clientY + document.documentElement.scrollTop
      this.left = this.startX
      this.top = this.startY
      this.lastMouseX = this.startX
      this.lastMouseY = this.startY
      this.width = 0
      this.height = 0

      // if (e.stopPropagation) e.stopPropagation()
      // if (e.preventDefault) e.preventDefault()
    },
    handleMove (e) {
      if (!this.handle) return
      console.log('dmmouseselect handleMove')
      console.log(e.pageX || e.clientX + document.documentElement.scrollLeft)
      this.lastMouseX = e.pageX - 8 || e.clientX + document.documentElement.scrollLeft - 8
      this.lastMouseY = e.pageY - 8 || e.clientY + document.documentElement.scrollTop - 8
      if (this.lastMouseX < this.startX) {
        this.width = this.startX - this.lastMouseX
        this.left = this.lastMouseX
      } else {
        this.width = this.lastMouseX - this.startX
        this.left = this.startX
      }
      if (this.lastMouseY < this.startY) {
        this.height = this.startY - this.lastMouseY
        this.top = this.lastMouseY
      } else {
        this.height = this.lastMouseY - this.startY
        this.top = this.startY
      }
      this.display = 'block'
      console.log('dmmouseselect width ' + this.startX)
      if (e.stopPropagation) e.stopPropagation()
      if (e.preventDefault) e.preventDefault()
    },
    handleUp () {
      clearTimeout(dmMouseSelectDown)
      console.log('dmmouseselect handleUp')
      this.display = 'none'
      let rec = {
        x1: this.left,
        y1: this.top - this.itop,
        x2: this.left + this.width,
        y2: this.top + this.height - this.itop
      }
      if (this.handle) {
        this.$emit('selectover', rec)
      }
      this.handle = false
    },
    handleNone () {
      this.handleUp()
    }
  }
}
</script>

<style scoped>
.mouseselect {
  border:solid 1px #000000;
  position: absolute;
  z-index: 999999;
}
</style>
