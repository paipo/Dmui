<template>
    <span class="dbtn" :class="s" ></span>
</template>

<script>
export default {
  name: 'dmBtns',
  data () {
    return {
      s: this.ds
    }
  },
  props: [
    'ds'
  ]
}
</script>

<style>
.del{
  background-image: url(../assets/images/close.png);
}
.add{
  background-image: url(../assets/images/add.png);
}
.dbtn{
  background-size: 100%;
  height: 18px;
  width: 18px;
  display: block;
  cursor: pointer;
}
</style>