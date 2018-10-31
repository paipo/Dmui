<template>
  <div class="one">
    <div class="wht_lg"></div>
    <div class="wht_c">17 C</div>
    <div class="wht_tip">多云</div>
    <div class="wht_dq">成都</div>
  </div>
</template>

<script>
export default {
  name: 'dmWeather',
  data () {
    return {
      isShow: false
    }
  },
  props: ['title', 'dq', 'dq2', 'type'],
  computed: {
  },
  methods: {
  }
}
</script>

<style scoped>
  .one {
    text-align: center;
  }
  .wht_c {
    height: 60%;
    line-height: 100%;
    font-size: 37px;
    float: right;
    position: absolute;
  }
  .wht_dq {
    height: 20%;
    line-height: 100%;
    clear: both;
  }
  .wht_tip {
    height: 20%;
    line-height: 100%;
    clear: both;
  }
  .wht_lg{
    background-color: #ccc;
    height: 100px;
    float: left;
    height: 60%;
    width: 100%;
  }
</style>
