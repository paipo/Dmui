<template>
  <div class="dmti_one" @mouseover="overthis" @mouseout="outthis">
    <input v-if="editTitle === true && dom !== 'inputline'" type="text" v-model="dtitle" class="dmti_title"/>
    <label v-else-if="editTitle === false && dom !== 'inputline'" type="text" class="dmti_label">{{dtitle}}</label>
    <select v-if="dom === 'select'" class="dmti_select" v-model="dvalue1">
      <option v-for="(item, index) in selectdatas" v-bind:key="index" name="nbfontsize" :value="item" :style="{fontSize:item+'px'}">{{item}}</option>
    </select>
    <input v-if="dom === 'inputline'" type="text" v-model="dvalue1" class="dmti_value"/>
    <input v-if="dom === 'input'" type="text" v-model="this.ddvalue1" class="dmti_value"/>
    <dmColorPicker v-if="dom === 'color'" v-model="dvalue1" class="dmcolor"></dmColorPicker>
    <dmSlider v-if="dom === 'slider'" v-model="dvalue1" :min="0" :max="100" class="dmsilder"></dmSlider>
    <input v-if="dom === 'checkbox'" type="checkbox" v-model="dvalue1" class="dmti_check"/>
    <div v-if="dom === 'image'" class="dmti_image" :title="dvalue1">
      <img v-if="dvalue != ''" :src="dvalue1"/>
    </div>
    <div v-if="dom === 'movie'" class="dmti_image" :title="dvalue1">
      <img v-if="dvalue1 != ''" src="../assets/images/movie.png"/>
    </div>
    <input v-if="dom === 'inputcolor'" type="text" v-model="dvalue1" class="dmti_inputcolor"/>
    <dmColorPicker v-if="dom === 'inputcolor'" v-model="dvalue2" class="dminputcolor"></dmColorPicker>
    <dmBtns ds="del" v-if="show_del === true && dom === 'inputcolor'" @click.native="clearvalue" class="btndel1"></dmBtns>
    <dmBtns ds="del" v-if="show_del === true && dom !== 'inputcolor'" @click.native="clearvalue" class="btndel2"></dmBtns>
  </div>
</template>

<script>
export default {
  name: 'dmTitleInput2',
  data () {
    console.log('dmTitleInput dom ' + this.ddom)
    return {
      isShow: false,
      editTitle: this.dedittitle,
      selectdatas: this.dselectdatas,
      dom: this.ddom,
      show_del: false,
      enabledel: this.denabledel,
      ddvalue1: this.dvalue1
    }
  },
  props: [
    'dtitle',
    'dvalue1',
    'dvalue2',
    'dedittitle',
    'dindex',
    'dselectdatas',
    'ddom',
    'denabledel',
    'cusclear'
  ],
  computed: {
  },
  methods: {
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
        this.dvalue1 = ''
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
      return this.dtitle
    },
    getValue () {
      return this.dvalue1
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
.dmti_one{
  position: relative;
  line-height: 40px;
  font-size: 14px;
  padding-left: 5px;
  padding-right: 5px;
  margin-bottom: 10px;
}
.dmcolor{
  margin-left: 20px;
}
.dmsilder{
  margin-left: 20px;
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
  font-size: 14px;
}
.dmti_label{
  float: left;
  width: 30%;
  height: 35px;
  border: none;
  background-color: #ffffff;
  text-align: center;
  font-size: 14px;
  line-height: 34px;
  color: #cccccc;
}
.dmti_value{
  float: left;
  width: 66%;
  height: 35px;
  border: none;
  border-bottom: solid 1px #eeeeee;
  margin-left: 4%;
  text-indent: 5px;
}
.dmti_inputcolor{
  float: left;
  width: 40%;
  height: 35px;
  border: none;
  border-bottom: solid 1px #eeeeee;
  margin-left: 4%;
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
  width: 66%;
  height: 35px;
  border: solid 1px #dddddd;
  margin-left: 4%;
  text-indent: 5px;
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
