<template>
    <div class="dbb" :style="{height:sheight+'px',width:swidth+'px'}">
      <span class="dbtn" :class="s" :style="{height:(sheight-14)+'px',width:(swidth-14)+'px'}"></span>
    </div>
</template>

<script>
export default {
  name: 'dmTips',
  data () {
    return {
      s: this.ds,
      sheight: this.height,
      swidth: this.width
    }
  },
  props: {
    // 默认
    ds: {
      type: String,
      default: ''
    },
    // 默认
    height: {
      type: Number,
      default: 18
    },
    // 默认
    width: {
      type: Number,
      default: 18
    }
  }
}
</script>

<style scoped>
.del{
  background-image: url(../assets/images/close.png);
}
.add{
  background-image: url(../assets/images/add.png);
}
.remove{
  background-image: url(../assets/images/remove.png);
}
.linebottom{
  background-image: url(../assets/images/linebottom.png);
}
.lineleft{
  background-image: url(../assets/images/lineleft.png);
}
.linemidel{
  background-image: url(../assets/images/linemidel.png);
}
.lineright{
  background-image: url(../assets/images/lineright.png);
}
.linetop{
  background-image: url(../assets/images/linetop.png);
}
.linever{
  background-image: url(../assets/images/linever.png);
}
.redo{
  background-image: url(../assets/images/redo.png);
}
.tobottom{
  background-image: url(../assets/images/tobottom.png);
}
.totop{
  background-image: url(../assets/images/totop.png);
}
.undo{
  background-image: url(../assets/images/undo.png);
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