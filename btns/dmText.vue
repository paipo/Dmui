<template>
  <div class="tel">
    <button v-if="v === 'ok'" @click="click" class="dmbtn_ok">{{text}}</button>
    <button v-if="v === 'canel'" @click="click" class="dmbtn_canel">{{text}}</button>
  </div>
</template>

<script>
export default {
  name: 'dmText',
  data () {
    return {
      text: this.dtext
    }
  },
  props: [
    'dtext',
    'v'],
  methods: {
    click () {
      this.$emit('dclick')
    }
  }
}
</script>

<style scoped>
.dmbtn_ok{
  height: 30px;
  line-height: 30px;
  border: none;
  background-color: #1B1B1B;
  color: #fff;
  outline:none;
}
.dmbtn_ok:hover{
  background-color: #444444;
}
.dmbtn_canel{
  height: 30px;
  line-height: 30px;
  border: none;
  background-color: #cccccc;
  color: #1B1B1B;
  outline:none;
}
.dmbtn_canel:hover{
  background-color: #eeeeee;
}
.dbtn{
  background-size: 100%;
  display: inline-block;
}
.dbb{
  display: flex;
  justify-content:center;
  align-items:Center;    
}
.dbb:hover{
  background-color: #eeeeee;
}
</style>