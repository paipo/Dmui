<template>
  <div id="dmWindowBar">
    <div id="dmlogo">
      <img style="height:100%;height:100%" src="../assets/images/logo.png" />
    </div>
    <div id="dmmenu">
      <dmMenu :items="items" @onClick="menuClick" />
      <!-- <div class="menuone">文件
        <dmMenu />
      </div>
      <div class="menuone"><img style="height:26px;margin-right:10px" src="../assets/images/接口.png" />接口
      </div>
      <div class="menuone"><img style="height:19px;width:19px;margin-right:10px" src="../assets/images/预览.png" />预览</div> -->
    </div>
    <div id="drag"></div>
    <div id="dmbtns">
      <span class="btns" @click="min">
        <img style="height:15px;width:15px;" src="../assets/images/最小化.png" />
      </span>
      <span class="btns" @click="max">
        <img style="height:16px;width:16px;" src="../assets/images/最大化.png" />
      </span>
      <span class="btns" @click="close">
        <img style="height:12px;width:12px;" src="../assets/images/关闭.png" />
      </span>
    </div>
  </div>
</template>
<script>
  const {ipcRenderer: ipc} = require('electron')
  export default {
    name: 'dmWindowBar',
    data () {
      return {
        items: [
          {
            text: '文件',
            icon: '',
            items: [
              {
                text: '新建',
                click: 'new'
              },
              {
                text: '打开',
                line: 'true',
                click: 'open'
              },
              {
                text: '退出',
                click: 'out'
              }
            ]
          },
          {
            text: '接口',
            icon: '../plugin/dmui/assets/images/接口.png',
            iconheight: 26,
            items: [
              {
                text: '测试',
                click: 'apitest'
              },
              {
                text: '设置',
                click: 'apiset'
              }
            ]
          },
          {
            text: '预览',
            icon: '../plugin/dmui/assets/images/预览.png',
            iconheight: 19,
            click: 'see'
          }
        ]
      }
    },
    methods: {
      menuClick: function (t) {
        switch (t) {
          case 'out': close()
        }
      },
      min: function () {
        ipc.send('min')
      },
      close: function () {
        ipc.send('close')
      },
      max: function () {
        ipc.send('max')
      }
    }
  }
</script>
    
<style scoped>
.menudown{
  list-style: none;
  padding: 0px;
  margin: 0px;
  background-color: #1B1B1B;
  position: absolute;
  top: 40px;
  width: 160px;
  box-shadow: 2px 2px 0px #cccccc;
  text-indent: 20px;
}
.mone:hover{
  background-color: #444444;
}
#dmlogo{
  height: 26px;
  width: 26px;
  margin-left: 10px;
  margin-top: 7px;
  margin-right: 10px;
}
#dmmenu{
  height: 40px;
}

#dmbtns{
  height: 40px;
  width: 150px;
  /* right: 0;
  position: absolute;
  top:0px; */
}
.btns{
  width: 50px;
  float: left;
  height: 40px;
  display: flex;
  justify-content:center;
  align-items:Center;
}
.btns:hover{
  float: left;
  background-color: #444444;
}
#dmWindowBar {
  z-index: 9999999;
  position: fixed;
  left:0px;
  right: 0px;
  top:0px;
  width: 100%;
  height: 40px;
  background-color: #2b2b2b;
  user-select:none;
  display: flex;
  flex-flow:row;
}
#drag{
  -webkit-app-region: drag;
  height: 40px;
  justify-content:center;
  display:flex;
  flex: 1 1 auto;
}
</style>