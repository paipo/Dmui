<template>
  <div class="dmti_one" @mouseover="overthis" @mouseout="outthis">
    <input v-if="editTitle === true && dom !== 'inputline'" type="text" v-model="ttitle" class="dmti_title"/>
    <label v-else-if="editTitle === false && dom !== 'inputline'" type="text" class="dmti_label">{{ttitle}}</label>
    <select v-if="dom === 'select'" class="dmti_select" v-model="tvalue">
      <option v-for="(item, index) in selectdatas" v-bind:key="index" name="nbfontsize" :value="selectValue(item)" :style="{fontSize:item+'px'}">{{selectText(item)}}</option>
    </select>
    <dmFontEdit v-if="dom === 'font'" :dfont="font" :dfonts="remote.getGlobal('fonts')" :di="fonti" :db="fontb" :dcolor="fontcolor" :dsize="fontsize"  @onChange="onChangeFont"/>
    <input v-if="dom === 'inputline'" type="text" v-model="tvalue" class="dmti_value"/>
    <input v-if="dom === 'input'" type="text" v-model="tvalue" class="dmti_value"/>
    <dmColorPicker v-if="dom === 'color'" v-model="tvalue" class="dmcolor"></dmColorPicker>
    <dmSlider v-if="dom === 'slider'" v-model="tvalue" :min="0" :max="100" class="dmsilder"></dmSlider>
    <input v-if="dom === 'checkbox' || dom === 'checkbox_color_select'" type="checkbox" v-model="tvalue" class="dmti_check"/>
    <dmColorPicker v-if="dom === 'color_select'" v-model="tvalue2" class="dminputcolor"></dmColorPicker> 
     <select v-if="dom === 'color_select'" class="dmti_selectm" v-model="tvalue3">
      <option v-for="(item, index) in selectdatas" v-bind:key="index" name="nbfontsize" :value="item">{{item}}</option>
    </select>

    <!-- <input v-if="dom === 'checkbox_color_select'" type="checkbox" v-model="tvalue" class="dmti_check"/> -->
    <div v-if="dom === 'image'" class="dmti_image" :title="tvalue">
      <img v-if="tvalue != ''" :src="tvalue"/>
    </div>
    <div v-if="dom === 'movie'" class="dmti_image" :title="tvalue">
      <img v-if="tvalue != ''" src="../assets/images/movie.png"/>
    </div>
    <input v-if="dom === 'inputcolor'" type="text" v-model="tvalue" class="dmti_inputcolor"/>
    <dmColorPicker v-if="dom === 'inputcolor'" v-model="tvalue2" class="dminputcolor"></dmColorPicker>
    <dmBtns ds="del" v-if="show_del === true && dom === 'inputcolor'" @click.native="clearvalue" class="btndel1"></dmBtns>
    <dmBtns ds="del" v-else-if="show_del === true && dom !== 'inputcolor'" @click.native="clearvalue" class="btndel2"></dmBtns>
  </div>
</template>

<script>
const remote = require('electron').remote
export default {
  name: 'dmTitleInput',
  data () {
    console.log('dmTitleInput dom ' + this.ddom)
    return {
      remote: remote,
      isShow: false,
      editTitle: this.dedittitle,
      ttitle: this.dtitle,
      tvalue: this.dvalue,
      tvalue1: this.dvalue1,
      tvalue2: this.dvalue2,
      tvalue3: this.dvalue3,
      index: this.dindex,
      index2: this.dindex2,
      selectdatas: this.dselectdatas,
      dom: this.ddom,
      show_del: false,
      enabledel: this.denabledel,
      font: this.dfont,
      fonti: this.dfonti,
      fontb: this.dfontb,
      fontsize: this.dfontsize,
      fontcolor: this.dfontcolor,
      fonts: this.dfonts
    }
  },
  props: [
    'dtitle',
    'dvalue',
    'dvalue1',
    'dvalue2',
    'dvalue3',
    'dedittitle',
    'dindex',
    'dindex2',
    'dselectdatas',
    'ddom',
    'denabledel',
    'cusclear',
    'dfont',
    'dfontb',
    'dfonti',
    'dfontsize',
    'dfontcolor',
    'dfonts'
  ],
  computed: {
  },
  watch: {
    ttitle (val) {
      console.log(val, 'ttitle')
      if (this.index >= 0) {
        let value = {
          value: val,
          index: this.index,
          index2: this.index2
        }
        this.$emit('onChangeTitle', value)
      } else {
        this.$emit('onChangeTitle', val)
      }
    },
    tvalue (val) {
      console.log(val, 'tvalue')
      if (this.index >= 0) {
        let value = {
          value: val,
          index: this.index,
          index2: this.index2
        }
        this.$emit('onChangeValue', value)
      } else {
        this.$emit('onChangeValue', val)
      }
    },
    tvalue1 (val) {
      console.log(val, 'tvalue1')
      if (this.index >= 0) {
        let value = {
          value: val,
          index: this.index,
          index2: this.index2
        }
        this.$emit('onChangeValue1', value)
      } else {
        this.$emit('onChangeValue1', val)
      }
    },
    tvalue2 (val) {
      console.log(val, 'tvalue2')
      if (this.index >= 0) {
        let value = {
          value: val,
          index: this.index,
          index2: this.index2
        }
        this.$emit('onChangeValue2', value)
      } else {
        this.$emit('onChangeValue2', val)
      }
    },
    tvalue3 (val) {
      console.log(val, 'tvalue3')
      if (this.index >= 0) {
        let value = {
          value: val,
          index: this.index,
          index2: this.index2
        }
        this.$emit('onChangeValue3', value)
      } else {
        this.$emit('onChangeValue3', val)
      }
    },
    dvalue (val) {
      this.tvalue = val
    },
    dvalue1 (val) {
      this.tvalue1 = val
    },
    dvalue2 (val) {
      this.tvalue2 = val
    },
    dvalue3 (val) {
      this.tvalue3 = val
    },
    dtitle (val) {
      this.ttitle = val
    }
  },
  methods: {
    selectValue (val) {
      if (val.value === undefined) {
        return val
      } else {
        return val.value
      }
    },
    selectText (val) {
      if (val.text === undefined) {
        return val
      } else {
        return val.text
      }
    },
    onChangeFont (val) {
      // this.font = val.font
      // this.fontb = val.b
      // this.fonti = val.i
      // this.fontcolor = val.color
      // this.fontsize = val.size
      this.$emit('onChangeValue', val)
    },
    mvalue (val) {
      if (this.index >= 0) {
        let value = {
          value: val,
          index: this.index
        }
        this.$emit('onChangeValue', value)
      } else {
        this.$emit('onChangeValue', val)
      }
    },
    clearvalue () {
      let func = typeof this.cusclear
      if (func === undefined) {
        this.tvalue = ''
      } else {
        this.cusclear(this.index)
      }
    },
    overthis () {
      if (!this.enabledel) return
      this.show_del = true
    },
    outthis () {
      if (!this.enabledel) return
      this.show_del = false
    },
    chageTitle () {
      console.log('chageTitle ' + this.dtitle)
    },
    chageValue () {
      console.log('chageValue ' + this.dvalue)
    },
    getTitle () {
      return this.ttitle
    },
    getValue () {
      return this.tvalue
    }
  }
}
</script>

<style>
.btndel1{
  float: right;
  cursor: pointer;
  margin-top: 8px;
  position: relative;
}
.btndel2{
  float: right;
  cursor: pointer;
  margin-top: -27px;
  position: relative;
}
.btndel3{
  float: right;
  cursor: pointer;
  margin-top: 20px;
  position: absolute;
}
.dmti_one{
  position: relative;
  line-height: 40px;
  font-size: 12px;
  padding-left: 5px;
  padding-right: 5px;
  margin-bottom: 10px;
}
.dmcolor{
  margin-left: 10px;
  width: 64%;
}
.dmsilder{
  margin-left: 10px;
  width: 58%;
  float: left;
  margin-top: 6px;
}
.dmti_title{
  float: left;
  width: 30%;
  height: 35px;
  border: none;
  border-bottom: solid 1px #eeeeee;
  text-indent: 5px;
  font-size: 12px;
}
.dmti_label{
  float: left;
  width: 30%;
  height: 35px;
  border: none;
  background-color: transparent;
  text-align: center;
  font-size: 12px;
  line-height: 34px;
  color: #999999;
}
.dmti_value{
  float: left;
  width: 60%;
  height: 35px;
  border: none;
  border-bottom: solid 1px #eeeeee;
  margin-left: 4%;
  text-indent: 5px;
  font-size: 12px;
  background-color: transparent;
}
.dmti_inputcolor{
  float: left;
  width: 40%;
  height: 35px;
  border: none;
  border-bottom: solid 1px #eeeeee;
  margin-left: 10px;
  text-indent: 5px;
}
.dminputcolor{
  margin-left: 10px;
  width: 25px;
  float: left;
  margin-top: 10px;
}
.dmti_select{
  float: left;
  width: 64%;
  height: 30px;
  border: solid 1px #dddddd;
  margin-left: 4%;
  text-indent: 5px;
  margin-top: 2px;
  border-radius: 3px;
  line-height: 30px;
}
.dmti_selectm{
  float: left;
  width: 60px;
  height: 18px;
  border: solid 1px #dddddd;
  margin-left: 10px;
  text-indent: 5px;
  margin-top: 8px;
  border-radius: 3px;
  line-height: 18px;
  font-size: 11px;
  text-align: center;
}
.dmti_check{
  float: left;
  height: 35px;
  border: solid 1px #dddddd;
  margin-left: 4%;
  text-indent: 5px;
}
.dmti_image{
  float: left;
  height: 35px;
  width: 35px;
  border: solid 1px #dddddd;
  margin-left: 4%;
  text-indent: 5px;
  cursor: pointer;
}
.dmti_image img{
  height: 100%;
  width: 100%;
  float: left;
}
.tipOneOk{
  background-color: #99CC99;
  color: #ffffff;
}
.tipOneEro{
  background-color: #FF6666;
  color: #ffffff;
}
.tipOneNone{
  background-color: #eeeeee;
  color: #777777;
}
</style>
