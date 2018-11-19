<template>
  <ul class="dm-g">
    <li v-for="(item) in list" v-bind:key="item.id" class="dm-g-one" @click="clickRow(item)">
      <div v-if="item.select" class="selected">
        <span class="one ig">
          <img :src="img(item.t)"/>
        </span>
        <span class="one o2">{{item.uid+1}}</span>
        <span class="one o1">{{item.tn}}</span>
        <span class="one o3"><img src="../../../static/images/more.png"/></span>
      </div>
      <div v-else class="selectno">
        <span class="one ig">
          <img :src="img(item.t)"/>
        </span>
        <span class="one o2">{{item.uid+1}}</span>
        <span class="one o1">{{item.tn}}</span>
        <span class="one o3"><img src="../../../static/images/more.png"/></span>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  name: 'dmGrid',
  data () {
    return {
      isShow: false
    }
  },
  props: ['list'],
  computed: {
  },
  methods: {
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
  background-color: #49443E;
  width: 100%;
  display: flex;
  justify-content:flex-start;
  align-items:Center; 
  color: #ffffff;
}
.selectno{
  background-color: #1B1B1B;
  width: 100%;
  display: flex;
  justify-content:flex-start;
  align-items:Center; 
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
  background-color: #49443E;
  color: #ffffff;
}
.dm-g-one .one{
  float: left;
  font-size: 12px;
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
  width: 60%;
  margin-left: 10px;
}
.o2{
  display: inline-block;
  width: 20px;
  text-align: center;
  margin-left: 10px;
  font-size: 14px;
  font-family: Arial, Helvetica, sans-serif;
}
.ig{
  height: 26px;
  width: 26px;
  margin-left: 10px;
  border-radius: 28px;
  background-color: #ffffff;
  display: flex;
  justify-content:center;
  align-items:Center; 
  border:solid 1px #49443E;
}
.o3{
  height: 10px;
  width: 20px;
  border-radius: 8px;
  background-color: #ffffff;
  display: flex;
  justify-content:center;
  align-items:Center;
}
.o3 img{
  height: 10px;
  cursor: pointer;
}
.ig img{
  width: 20px;
}
</style>
