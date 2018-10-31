<template>
 <div class="dicon" :style="{display:display,left:sleft(),top:stop()}">
   <img :src="iconimage()" />
 </div>
</template>

<script>

export default {
  name: 'dmMouseStyle',
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
      handle: false,
      icon: this.dicon
    }
  },
  props: [
    'body',
    'dicon',
    'tip',
    'itop'
  ],
  computed: {
  },
  methods: {
    iconimage () {
      return this.icon
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
      console.log('dmMouseStyle start')
      // document.addEventListener('touchend touchcancel', this.handleBegin, true)
      if (this.body === '') {
        // document.addEventListener('mousedown', this.handleDown, true)
        document.addEventListener('mousemove', this.move, true)
        document.addEventListener('mouseup', this.endClick, true)
      } else {
        // document.getElementById(this.body).addEventListener('mousedown', this.handleDown, true)
        document.getElementById(this.body).addEventListener('mousemove', this.move, true)
        document.getElementById(this.body).addEventListener('mouseup', this.endClick, true)
      }
    },
    begin (icon) {
      console.log('dmMouseStyle begin')
      this.icon = icon
      this.handle = true
      // console.log('dmMouseStyle hadleBegin')
      // console.log(e.pageX || e.clientX + document.documentElement.scrollLeft)

      // this.startX = e.pageX || e.clientX + document.documentElement.scrollLeft
      // this.startY = e.pageY || e.clientY + document.documentElement.scrollTop

      // this.handle = true

      // this.left = this.startX
      // this.top = this.startY
      // this.lastMouseX = this.startX
      // this.lastMouseY = this.startY
      // this.width = 0
      // this.height = 0
    },
    move (e) {
      if (!this.handle) return
      console.log('dmMouseStyle move')
      console.log(e.pageX || e.clientX + document.documentElement.scrollLeft)
      this.left = e.pageX - 8 || e.clientX + document.documentElement.scrollLeft - 8
      this.top = e.pageY - 8 || e.clientY + document.documentElement.scrollTop - 8
      this.display = 'block'
      if (e.stopPropagation) e.stopPropagation()
      if (e.preventDefault) e.preventDefault()
    },
    endClick (e) {
      console.log('dmMouseStyle handleUp')
      this.display = 'none'
      if (this.handle) {
        this.$emit('endClick', this.left, this.top, this.tip)
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
.dicon {
  position: absolute;
  background-size: 100%;
  z-index: 999;
  width: 28px;
  height: 28px;
  border-radius: 30px;
  display: flex;
  justify-content:center;
  align-items:Center;
  background-color: #ffffff;
  border:solid 1px #49443E;
  text-align: center;
  line-height: 20px;
}
.dicon img{
  width: 20px;
  display:inline-block;
  vertical-align:middle;
}
</style>
