<template>
  <div class="tel">
    <div class="menuone" v-for="(item) in mitems" v-bind:key="item.uid" @click="click(item)" @mouseenter="enter(item)">
      <img v-if="item.icon" :style="{height:item.iconheight + 'px'}" style="margin-right:10px" v-bind:src="item.icon" />{{item.text}}
      <div v-if="item.menus" class="menumore" :style="{marginLeft: mleft(item), display: display(item.menus.show)}">
        <div class="m2" v-for="(item2) in item.menus.items" v-bind:key="item2.uid"  @click.stop="click2(item, item2)">
          {{item2.text}}
          <div v-if="item2.menus" class="menumore2" :style="{display: display2(item2.menus.show)}">
            <div class="m2" v-for="(item3) in item2.menus.items" v-bind:key="item3.uid" @click.stop="click3(item3)">{{item3.text}}</div>
          </div>
          <div v-if="item2.line === 'true'" class="line"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'dmMenu',
  data () {
    let datas = this.items
    // this.items.forEach(function (c) {
    //   let one = c
    //   if (c.items) {
    //     let ones = {
    //       ms: c.items,
    //       show: false
    //     }
    //     c.items.forEach(function (c3) {
    //       if (c3.items) {
    //         let ones3 = {
    //           ms: c3.items,
    //           show: false
    //         }
    //         one.items = ones
    //       }
    //     })
    //     one.items = ones
    //   }
    //   datas.push(one)
    // })
    // console.log(datas)
    return {
      mitems: datas,
      iniIn: false
    }
  },
  props: ['items'],
  beforeMount () {
    this._close = e => {
      // 如果点击发生在当前组件内部，则不处理
      if (this.$el.contains(e.target)) {
        this.iniIn = true
        return
      }
      this.iniIn = false
      this.items.forEach(function (c) {
        if (c.menus) {
          c.menus.show = false
          c.menus.items.forEach(function (c2) {
            if (c2.menus) {
              c2.menus.show = false
            }
          })
        }
      })
    }
    document.body.addEventListener('click', this._close)
  },
  beforeDestroy () {
    document.body.removeEventListener('click', this._close)
  },
  methods: {
    out (val) {
      // val.menus.show = false
    },
    display (val) {
      if (val === true) {
        return ''
      } else {
        return 'none'
      }
    },
    display2 (val) {
      if (val === true) {
        return ''
      } else {
        return 'none'
      }
    },
    enter (val) {
      if (this.iniIn) {
        this.click(val)
      }
    },
    click (val) {
      this.items.forEach(function (c) {
        if (val !== c) {
          if (c.menus) {
            c.menus.show = false
            c.menus.items.forEach(function (c2) {
              if (c2.menus) {
                c2.menus.show = false
              }
            })
          }
        }
      })
      if (val.click) {
        this.$emit('onClick', val.click)
        if (val.menus) {
          val.menus.show = false
        }
      } else {
        if (val.menus) {
          if (val.menus.show === true) {
            val.menus.show = false
          } else {
            val.menus.show = true
          }
        }
      }
    },
    click2 (val1, val2) {
      this.items.forEach(function (c) {
        if (c.menus) {
          c.menus.items.forEach(function (c2) {
            if (val2 !== c2) {
              if (c2.menus) {
                c2.menus.show = false
              }
            }
          })
        }
      })
      if (val2.click) {
        this.$emit('onClick', val2.click)
        val1.menus.show = false
      } else {
        if (val2.menus) {
          if (val2.menus.show === true) {
            val2.menus.show = false
          } else {
            val2.menus.show = true
          }
        }
      }
    },
    click3 (val) {
      this.items.forEach(function (c) {
        if (c.menus) {
          c.menus.show = false
          c.menus.items.forEach(function (c2) {
            if (c2.menus) {
              c2.menus.show = false
            }
          })
        }
      })
      if (val.click) {
        this.$emit('onClick', val.click)
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
.menumore2{
  position: absolute;
  background-color: #1B1B1B;
  width: 160px;
  margin-left: 160px;
  margin-top: -40px;
  text-indent: 40px;
  box-shadow: 2px 3px 0px #cccccc;
}
.menumore2 .m2:hover{
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