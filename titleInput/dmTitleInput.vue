<template>
  <div class="dmti_one" @mouseover="overthis" @mouseout="outthis">
    <input v-if="editTitle === true" type="text" v-model="ttitle" class="dmti_title"/>
    <label v-else-if="editTitle === false" type="text" class="dmti_label">{{ttitle}}</label>
    <select v-if="dom === 'select'" class="dmti_select" v-model="tvalue">
      <option v-for="(item, index) in selectdatas" v-bind:key="index" name="nbfontsize" :value="item" :style="{fontSize:item+'px'}">{{item}}</option>
    </select>
    <input v-if="dom === 'input'" type="text" v-model="tvalue" class="dmti_value"/>
    <dmColorPicker v-if="dom === 'color'" v-model="tvalue" class="dmcolor"></dmColorPicker>
    <dmSlider v-if="dom === 'slider'" v-model="tvalue" :min="0" :max="100" class="dmsilder"></dmSlider>
    <dmBtns ds="del" v-if="show_del === true" @click.native="clearvalue" class="btndel"></dmBtns>
  </div>
</template>

<script>
export default {
  name: 'dmTitleInput',
  data () {
    return {
      isShow: false,
      editTitle: this.dedittitle,
      ttitle: this.dtitle,
      tvalue: this.dvalue,
      index: this.dindex,
      selectdatas: this.dselectdatas,
      dom: this.ddom,
      show_del: false,
      enabledel: this.denabledel
    }
  },
  props: [
    'dtitle',
    'dvalue',
    'dedittitle',
    'dindex',
    'dselectdatas',
    'ddom',
    'denabledel',
    'cusclear'
  ],
  computed: {
  },
  watch: {
    ttitle (val) {
      console.log(val, 'ttitle')
      if (this.index >= 0) {
        let value = {
          value: val,
          index: this.index
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
          index: this.index
        }
        this.$emit('onChangeValue', value)
      } else {
        this.$emit('onChangeValue', val)
      }
    },
    dvalue (val) {
      this.tvalue = val
    },
    dtitle (val) {
      this.ttitle = val
    }
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
.btndel{
  float: right;
  cursor: pointer;
  margin-top: -27px;
  position: relative;
}
.dmti_one{
  position: relative;
  height: 40px;
  line-height: 40px;
  margin-top: 5px;
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
.dmti_select{
  float: left;
  width: 66%;
  height: 35px;
  border: solid 1px #dddddd;
  margin-left: 4%;
  text-indent: 5px;
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
