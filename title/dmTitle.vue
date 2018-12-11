<template>
  <div :style="dstyle" class="dtitle">
    {{dtitle}}
  </div>
</template>

<script>
export default {
  name: 'dmTitle',
  data () {
    return {
      isShow: false,
      dtype: '',
      dtext: ''
    }
  },
  props: ['dtitle', 'dstyle'],
  methods: {
  }
}
</script>

<style>
.dtitle{
  font-size: 17px;
  text-align: center;
  width: 100%;
  padding: 5px 0px 5px 0px;
}
</style>
