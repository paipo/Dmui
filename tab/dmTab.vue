<template> 
    <div class="my-tabs">
    <div class="tabs-bar">
      <div class="tabs-bar-nav">
        <div class="tabs-tab" v-for="tab in tabList" v-bind:key="tab.key"
        :class="[tabIndex == tab.index ? 'tabs-active' : '']"
        @click="changeTab(tab)" :style="{width: (100 / tabList.length) + '%'}">
          {{tab.name}}
        </div>
      </div>
    </div>
    <div class="tabs-content">
      <slot></slot>
    </div>
  </div>
</template> 
<script>
export default {
  name: 'dmTab',
  props:
  {
    tabList: Array,
    tabIndex: Number
  },
  data () {
    return {
    }
  },
  methods: {
    changeTab: function (tab) {
      this.$emit('changeTab', tab)
    }
  }
}
</script> 
<style scoped>
.my-tabs {
  font-size: 13px;
  color: #444;
}
 .tabs-bar {
   position: relative;
   height: 30px;
   box-sizing: border-box;
   width: 100%;
   line-height: 30px;
 }
 .tabs-bar-nav {
   display: table;
   position: absolute;
   width: 100%;
 }
 .tabs-tab {
   height: 30px;
   position: relative;
   display: inline-block;
   text-align: center;
   user-select:none;
   cursor: default;
   background-color: #444444;
   color: #ffffff;
 }
 .tabs-active {
   /* border-top: 1px solid pink;
   border-left: 1px solid pink;
   border-right: 1px solid pink;
   border-bottom: 1px solid #fff; */
   background-color: #ffffff;
   color: #444444;
 }
 .tabs-content {
   padding-top: 10px
 }
</style>
 

