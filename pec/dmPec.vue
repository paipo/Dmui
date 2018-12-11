<template>
  <div class="tel">
    <div class="mainbar" :style="stylemain()">
      <div class="pecbar" :style="stylebar()">
        <div class="pec">{{val}}%&nbsp;&nbsp;</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'dmPec',
  data () {
    return {
      val: 50,
      title: this.dtitle,
      value: this.dvalue
    }
  },
  props: ['width', 'height', 'titlemain', 'titletip', 'cur', 'max', 'radius', 'backcolor', 'peccolor', 'titlebkcolor', 'titlepeccolor'],
  mounted () {
  },
  methods: {
    stylemain () {
      let brres = ''
      if (this.radius) {
        brres = this.radius + 'px'
      } else {
        brres = '30px'
      }
      let bkcolor = ''
      if (this.backcolor) {
        bkcolor = this.backcolor
      } else {
        bkcolor = '#eeeeee'
      }
      let bkheight = ''
      if (this.height) {
        bkheight = this.height + 'px'
      } else {
        bkheight = '30px'
      }
      let bkwidth = ''
      if (this.width) {
        bkwidth = this.width + 'px'
      } else {
        bkwidth = '220px'
      }
      return {
        borderRadius: brres,
        backgroundColor: bkcolor,
        height: bkheight,
        width: bkwidth
      }
    },
    stylebar () {
      let brres = ''
      if (this.radius) {
        brres = this.radius + 'px'
      } else {
        brres = '30px'
      }
      let peccolor = ''
      if (this.peccolor) {
        peccolor = this.peccolor
      } else {
        peccolor = '#515151'
      }
      let pecmax = 100
      if (this.max) {
        pecmax = parseInt(this.max)
      }
      let peccur = 10
      if (this.cur) {
        peccur = parseInt(this.cur)
      }
      let bkheight = ''
      if (this.height) {
        bkheight = this.height
      } else {
        bkheight = '30px'
      }

      let _val
      if (pecmax > 0 && pecmax > peccur) {
        _val = (peccur / pecmax * 100).toFixed(0)
      } else {
        _val = 0
      }

      if (pecmax < peccur || _val > 100) {
        _val = 100
      }
      if (_val === 0) {
        _val = 10
      }
      let _w = _val + '%'
      this.val = _val
      console.log('one pec ' + this.val + ' ' + this.cur + ' ' + this.max)
      return {
        borderRadius: brres,
        backgroundColor: peccolor,
        width: _w,
        height: bkheight
      }
    }
  }
}
</script>

<style scoped>
.mainbar {
  min-height: 30px;
  min-width: 200px;
  background-color: #eeeeee;
  overflow: hidden;
}
.pecbar{
  height: 100%;
  display: flex;
  justify-content:flex-end;
  align-items:Center;
}
  .tel{
    width:100%;
  }
.pec{
  color:#ffffff;
  display: flex;
    justify-content:center;
    align-items:Center;
}
</style>