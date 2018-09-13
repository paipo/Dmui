<template>
  <ul class="dm-g">
    <li v-for="(item) in list" v-bind:key="item.id" class="dm-g-one">
      <span class="one">{{item.t}}</span>
      <span class="one">{{item.name}}</span>
      <span class="one">{{item.uid}}</span>
    </li>
  </ul>
</template>

<script>
export default {
  name: 'dmGrid',
  data () {
    return {
      isShow: false,
      list: []
    }
  },
  props: {
  },
  computed: {
  },
  methods: {
    bind (datas) {
      this.list = datas
    },
    add (data) {
      this.list.push(data)
    }
  }
}
</script>

<style>
::-webkit-scrollbar{
    width: 5px;
    background-color: #eeeeee;
}
::-webkit-scrollbar-track-piece{
    background: #eeeeee;
    -webkit-border-radius: 6px;
}
* {
  padding: 0;
  margin: 0;
}
.dm-g{
  overflow-y: scroll;
  overflow-x: hidden;
}
ul,li{
  list-style: 0px;
}
.dm-g-one{
  font-size: 14px;
  cursor: pointer;
  float: left;
  width: 100%;
  height: 30px;
  line-height: 30px;
  border-top: solid 1px #eeeeee;
  border-bottom: solid 1px #eeeeee;
  margin-bottom: -1px;
}
.dm-g-one:hover{
  background-color: #eeeeee;
}
.dm-g-one .one{
  float: left;
  margin-left: 10px;
}
</style>
