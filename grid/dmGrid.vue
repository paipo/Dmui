<template>
<div>
  <ul class="dm-g">
    <li v-for="(item, index) in list" v-bind:key="item.id" class="dm-g-one" @click.stop="clickRow(item)">
      <div :class="item.select ? 'selected' : 'selectno'">
        <span class="one ig">
          <img :src="img(item.t)"/>
        </span>
        <span class="one o2">{{item.uid+1}}</span>
        <span class="one o1">{{item.tn}}</span>
          <div class="one o4">
            <span :class="shows[index] ? 'i0' : 'i0b'">
              <img  src="../assets/images/修改.png" title="修改" @click="showUpdate(item)" />
            </span>
            <span :class="shows[index] ? 'i1' : 'i1b'">
              <img  src="../assets/images/接口.png" title="接口" />
            </span>
            <span :class="shows[index] ? 'i2' : 'i2b'">
              <img src="../assets/images/关闭.png" title="删除" />
            </span>
          </div>
        <span class="one o3">
          <span :class="shows[index] ? 'i3g' : 'i3'" @click="showMenu(index)">
            <img src="../../../static/images/more.png" title="更多功能"/>
          </span>
        </span>
      </div>
    </li>
  </ul>
  </div>
</template>

<script>
export default {
  name: 'dmGrid',
  data () {
    let len = this.list.length
    let _show = []
    for (let l = 0; l < len; l++) {
      _show.push(false)
    }
    return {
      showUpdates: false,
      shows: _show,
      menu: [
        {
          text: '接口',
          icon: '../plugin/dmui/assets/images/接口.png',
          iconheight: 19,
          click: 'ck-api'
        },
        {
          text: '刪除',
          icon: '../plugin/dmui/assets/images/关闭.png',
          iconheight: 8,
          click: 'ck-del'
        }
      ],
      isShow: false
    }
  },
  props: ['list'],
  computed: {
  },
  methods: {
    close () {
      this.showUpdates = false
    },
    showUpdate (item) {
      this.showUpdates = true
      this.$emit('showUpdate', true)
      // alert(item.tn)
    },
    showMenu (index) {
      if (this.shows[index]) {
        this.shows[index] = false
      } else {
        this.shows[index] = true
      }
    },
    menuClick (item) {
      this.$emit('clickOne', item)
    },
    img (t) {
      switch (t) {
        case 'chart_bar' : return __static + '\\images\\c_c_bar.png'
        case 'chart_pie' : return __static + '\\images\\c_c_pie.png'
        case 'chart_line' : return __static + '\\images\\c_c_line.png'
        case 'chart_radar' : return __static + '\\images\\c_c_radar.png'
        case 'chart_sunburst' : return __static + '\\images\\c_line.png'
        case 'text' : return __static + '\\images\\c_font.png'
        case 'image' : return __static + '\\images\\c_image.png'
        case 'movie' : return __static + '\\images\\c_movie.png'
        case 'stable' : return __static + '\\images\\c_table.png'
        case 'sum' : return __static + '\\images\\c_sum.png'
        case 'clock' : return __static + '\\images\\c_clock2.png'
        case 'date' : return __static + '\\images\\c_date.png'
        case 'pec' : return __static + '\\images\\c_pec.png'
      }
    },
    bind (datas) {
      let that = this
      datas.forEach(function (c) {
        let one = {
          uid: c.uid,
          t: c.t,
          name: c.name,
          select: false,
          tag: c
        }
        that.list.push(one)
      })
      // this.list = datas
    },
    add (data) {
      console.log('add ' + data.uid)
      let one = {
        uid: data.uid,
        t: data.t,
        name: data.name,
        select: false,
        tag: data
      }
      this.list.push(one)
      // this.list.push(data)
    },
    clickRow (item) {
      // this.list.forEach(function (c) {
      //   c.select = false
      // })
      // item.select = true
      this.$emit('clickRow', item)
    }
  }
}
</script>

<style scoped>
@keyframes maoXZ0{
  0%,5% {
    transform:rotate(360deg);
    left:120px;
    opacity:0;
  }
  10% {
    opacity:0;
  }
  95%,100%{
     transform:rotate(0deg);
     left:-10px;
     opacity:1;
  }
}
@keyframes maoXZ00{
  0%,5% {
    transform:rotate(0deg);
    left:0px;
    opacity:1;
  }
  50% {
    opacity:0;
  }
  95%,100%{
     transform:rotate(360deg);
     left:140px;
     opacity:0;
  }
}
@keyframes maoXZ1{
  0%,5% {
    transform:rotate(360deg);
    left:60px;
    opacity:0;
  }
  10% {
    opacity:0;
  }
  95%,100%{
     transform:rotate(0deg);
     left:0px;
     opacity:1;
  }
}
@keyframes maoXZ11{
  0%,5% {
    transform:rotate(0deg);
    left:0px;
    opacity:1;
  }
  50% {
    opacity:0;
  }
  95%,100%{
     transform:rotate(360deg);
     left:100px;
     opacity:0;
  }
}
@keyframes maoXZ22{
  0%,5% {
    transform:rotate(0deg);
    left:10px;
    opacity:1;
  }
  50% {
    opacity:0;
  }
  95%,100%{
     transform:rotate(360deg);
     left:100px;
     opacity:0;
  }
}
@keyframes maoXZ6{
  0%,5% {
    transform:rotate(360deg);
  }
  95%,100%{
     transform:rotate(0deg);
  }
}
@keyframes maoXZ5{
  0%,5% {
    transform:rotate(0deg);
  }
  95%,100%{
     transform:rotate(360deg);
  }
}
@keyframes maoXZ2{
  0%,5% {
    transform:rotate(360deg);
    left:60px;
    opacity:0;
  }
  10% {
    opacity:0;
  }
  95%,100%{
     transform:rotate(0deg);
     left:10px;
     opacity:1;
  }
}
@keyframes maoGO{
  0%,5% {
    left:60px
  }
  95%,100%{
    left:0px
  }
}
.i0{
  float: left;
  height: 20px;
  width: 20px;
  border-radius: 20px;
  border:solid 1px #fff;
  text-align: center;
  cursor: pointer;
  display: flex;
  justify-content:center;
  align-items:Center;
  position: relative;
  right: 10px;
  -webkit-animation: maoXZ0 0.6s 0s;
}
.i0b{
  float: left;
  height: 20px;
  width: 20px;
  border-radius: 20px;
  border:solid 1px #fff;
  text-align: center;
  cursor: pointer;
  display: flex;
  justify-content:center;
  align-items:Center;
  position: relative;
  left: 120px;
  -webkit-animation: maoXZ00 0.5s 0s;
}
.i1{
  float: left;
  height: 20px;
  width: 20px;
  border-radius: 20px;
  border:solid 1px #fff;
  text-align: center;
  cursor: pointer;
  display: flex;
  justify-content:center;
  align-items:Center;
  position: relative;
  -webkit-animation: maoXZ1 0.6s 0s;
}
.i1b{
  float: left;
  height: 20px;
  width: 20px;
  border-radius: 20px;
  border:solid 1px #fff;
  text-align: center;
  cursor: pointer;
  display: flex;
  justify-content:center;
  align-items:Center;
  position: relative;
  left: 100px;
  -webkit-animation: maoXZ11 0.5s 0s;
}
.i1 img, .i1b img {
  height: 15px;
}
.i0 img, .i0b img {
  height: 8px;
}
.i2{
  float: left;
  display: flex;
  justify-content:center;
  align-items:Center;
  height: 20px;
  width: 20px;
  border-radius: 20px;
  border:solid 1px #fff;
  text-align: center;
  cursor: pointer;
  left: 10px;
  position: relative;
  -webkit-animation: maoXZ2 0.6s 0s;
}
.i2b{
  float: left;
  display: flex;
  justify-content:center;
  align-items:Center;
  height: 20px;
  width: 20px;
  border-radius: 20px;
  border:solid 1px #fff;
  text-align: center;
  cursor: pointer;
  left: 10px;
  position: relative;
  left:100px;
  -webkit-animation: maoXZ22 0.5s 0s;
}
.i2 img,.i2b img {
  height: 8px;
}
.i3{
  display: flex;
  justify-content:center;
  align-items:Center;
  height: 20px;
  width: 20px;
  border-radius: 20px;
  background-color: #ffffff;
  -webkit-animation: maoXZ5 0.5s 0s;
}
.i3g{
  display: flex;
  justify-content:center;
  align-items:Center;
  height: 20px;
  width: 20px;
  border-radius: 20px;
  background-color: #ffffff;
  -webkit-animation: maoXZ6 0.6s 0s;
}
/*定义滚动条高宽及背景 高宽分别对应横竖滚动条的尺寸*/
.dm-g::-webkit-scrollbar
{
	width: 6px;
	height: 6px;
	background-color: #1B1B1B;
}
/*定义滚动条轨道 内阴影+圆角*/
.dm-g::-webkit-scrollbar-track
{
	-webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.1);
	border-radius: 10px;
	background-color: #1B1B1B;
  margin-top: 5px;
  margin-bottom: 5px;
}
/*定义滑块 内阴影+圆角*/
.dm-g::-webkit-scrollbar-thumb
{
	border-radius: 10px;
	-webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.1);
	background-color: #ffffff;
  margin-top: 5px;
  margin-bottom: 5px;
}
* {
  padding: 0;
  margin: 0;
}
.selected{
  background-color: #252525;
  width: 100%;
  display: flex;
  justify-content:flex-start;
  align-items:Center; 
  color: #ffffff;
}
.selected .o3{
  background-color: #252525;
}
.selectno{
  background-color: #1B1B1B;
  width: 100%;
  display: flex;
  justify-content:flex-start;
  align-items:Center; 
}
.selectno .o3{
  background-color: #1B1B1B;
}
.dm-g{
  overflow-y: scroll;
  overflow-x: hidden;
  color: #777;
}
ul,li{
  list-style: 0px;
}
.dm-g-one{
  float: left;
  width: 100%;
  height: 40px;
  line-height: 40px;
  color:#fff;
  cursor:default;
}
.dm-g-one .selectno:hover,.dm-g-one .selected:hover{
  background-color: #252525;
  color: #ffffff;
}
.selectno:hover .o3{
  background-color: #252525;
  color: #ffffff;
}
.dm-g-one .one{
  float: left;
  font-size: 12px;
  user-select: none;
}
.selecteheard{
  font-size: 12px;
  height: 30px;
  line-height: 30px;
  background-color: #1C243B;
  color:#fff;
}
.o1{
  display: inline-block;
  width: 95px;
  margin-left: 10px;
}
.o2{
  display: inline-block;
  width: 15px;
  text-align: center;
  margin-left: 10px;
  font-size: 14px;
  font-family: Arial, Helvetica, sans-serif;
}
.o4{
  display: inline-block;
  width: 75px;
  text-align: center;
  font-size: 14px;
  font-family: Arial, Helvetica, sans-serif;
  position: relative;
  -webkit-animation: maoGO 1s 0s;
}
.o4n{
  display: inline-block;
  width: 55px;
  text-align: center;
  font-size: 14px;
  font-family: Arial, Helvetica, sans-serif;
  position: relative;
}
.ig{
  height: 25px;
  width: 25px;
  margin-left: 5px;
  border-radius: 25px;
  background-color: #ffffff;
  display: flex;
  justify-content:center;
  align-items:Center; 
  border:solid 1px #49443E;
}
.o3{
  padding-right: 5px;
  width: 30px;
  display: flex;
  justify-content:flex-end;
  align-items:flex-end;
}
.o3 img{
  height: 10px;
  cursor: pointer;
  position: relative;
}
.ig img{
  width: 20px;
}
</style>
