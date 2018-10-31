<template>
  <div class="tel">
    <div class="menuone" v-for="(item) in mitems" v-bind:key="item.uid" @click="click(item)" @mouseenter="enter(item)">
      <img v-if="item.icon" :style="{height:item.iconheight + 'px'}" style="margin-right:10px" v-bind:src="item.icon" />{{item.text}}
      <div v-if="item.items" class="menumore" :style="{marginLeft: mleft(item), display: display(item.items.show)}" @mouseleave="out(item)">
        <div class="m2" v-for="(item) in item.items.ms" v-bind:key="item.uid" @click="click(item)">
          {{item.text}}
          <div v-if="item.line === 'true'" class="line"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'dmMenu',
  data () {
    let datas = []
    this.items.forEach(function (c) {
      let one = c
      if (c.items) {
        let ones = {
          ms: c.items,
          show: false
        }
        one.items = ones
      }
      datas.push(one)
    })
    console.log(datas)
    return {
      mitems: datas
    }
  },
  props: ['items'],
  methods: {
    out (val) {
      val.items.show = false
    },
    display (val) {
      if (val === true) {
        return ''
      } else {
        return 'none'
      }
    },
    enter (val) {
    },
    click (val) {
      this.items.forEach(function (c) {
        if (c.items) {
          c.items.show = false
        }
      })
      if (val.click) {
        this.$emit('onClick', val.click)
        val.items.show = false
      } else {
        val.items.show = true
      }
    },
    icon (item) {
      return item.icon
    },
    mleft (item) {
      if (item.icon) {
        return '-55px'
      } else {
        return '-20px'
      }
    }
  }
}
</script>

<style scoped>
 .menuone{
  font-size: 14px;
  color:#ffffff;
  padding: 0px 20px;
  float: left;
  height: 40px;
  line-height: 40px;
  cursor: default;
  display: flex;
  justify-content:center;
  align-items:Center;
}
.menuone:hover{
  background-color: #444444;
}
.menumore{
  position: absolute;
  background-color: #1B1B1B;
  width: 160px;
  top: 40px;
  text-indent: 40px;
  box-shadow: 2px 3px 0px #cccccc;
}
.menumore .m2{
  height: 40px;
}
.menumore .m2:hover{
  background-color: #444444;
}
.line{
  height: 1px;
  width: 120px;
  padding: 0px 20px;
  background-color: #ffffff;
  margin-left: 20px;
}
</style>