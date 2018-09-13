<template>
  <transition name="fade">
    <div class="tipOne" :class="pclass" :style="{display}" v-if="isShow">{{ptext}}</div>
  </transition>
</template>

<script>
export default {
  name: 'dmTip',
  data () {
    return {
      isShow: false,
      dtype: '',
      dtext: ''
    }
  },
  props: {
  },
  computed: {
    ptext () {
      return this.dtext
    },
    pclass () {
      if (this.dtype === 'ok') {
        return 'tipOneOk'
      } else if (this.dtype === 'ero') {
        return 'tipOneEro'
      } else {
        return 'tipOneNone'
      }
    }
  },
  methods: {
    showOk (text) {
      this.dtype = 'ok'
      this.dtext = text
      this.isShow = true
    },
    showEro (text) {
      this.dtype = 'ero'
      this.dtext = text
      this.isShow = true
    },
    show (text) {
      this.dtype = ''
      this.dtext = text
      this.isShow = true
    },
    hide () {
      this.isShow = false
    },
    _display (text) {
      this.dtext = text
      if (this.isShow) {
        this.isShow = false
      } else {
        this.isShow = true
      }
    },
    displayOk (text) {
      this.dtype = 'ok'
      this._display(text)
    },
    displayEro (text) {
      this.dtype = 'ero'
      this._display(text)
    },
    display (text) {
      this.dtype = ''
      this._display(text)
    }
  }
}
</script>

<style>
.fade-enter-active, .fade-leave-active {
  transition: all .3s ease;
}
.fade-leave-active {
  transform: translateY(-100px);
  opacity: 0;
}
.fade-enter {
  transform: translateY(-100px);
  opacity: 0;
}
.tipOne{
  height: 40px;
  border-radius: 20px;
  line-height: 36px;
  text-align: center;
  position: absolute;
  top: 20px;
  font-size: 14px;
  padding-left: 20px;
  padding-right: 20px;
  cursor: default;
  z-index: 999;
  border:solid 2px #ffffff;
}
.tipOneOk{
  background-color: #99CC99;
  color: #ffffff;
}
.tipOneEro{
  background-color: #FF6666;
  color: #ffffff;
}
.tipOneNone{
  background-color: #eeeeee;
  color: #777777;
}
</style>
