<template>
  <div class="tel">
    <div class="def" @click="displayDef()">
      <span class="tcolor" :style="{backgroundColor:value.color}"></span>
      <span style="float:left;">{{getText()}}</span>
    </div>
    <div class="set" v-if="this.showed === 'true'">
      <div class="l1">
        <span v-if="value.b === 'true'" class="btn s" @click="ckb()">B</span>
        <span v-else class="btn n" @click="ckb()">B</span>
        <span v-if="value.i === 'true'" class="btn s" @click="cki()">i</span>
        <span v-else class="btn n" @click="cki()">i</span>
      </div>
      <div class="l1">
        <span class="bt">颜色</span><dmColorPicker class="btn2" v-model="value.color"  @change="onChange()" />
      </div>
      <div class="l1">
        <select class="select" @change="onChange()" v-model="value.font">
          <option v-for="(i) in value.fonts" v-bind:key="i.key">{{i}}</option>
        </select>
      </div>
      <div class="l1">
        <span class="bt">大小</span><select class="select2" @change="onChange()" v-model="value.size">
          <option>9</option>
          <option>10</option>
          <option>11</option>
          <option>12</option>
          <option>13</option>
          <option>14</option>
          <option>15</option>
          <option>16</option>
          <option>17</option>
          <option>18</option>
          <option>19</option>
          <option>20</option>
          <option>21</option>
          <option>22</option>
          <option>24</option>
          <option>26</option>
          <option>27</option>
          <option>28</option>
          <option>30</option>
          <option>32</option>
          <option>34</option>
          <option>36</option>
          <option>38</option>
          <option>40</option>
          <option>42</option>
          <option>44</option>
          <option>46</option>
          <option>48</option>
          <option>50</option>
        </select>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'dmFontEdit',
  data () {
    let v = {
      font: '',
      b: false,
      i: false,
      size: 10,
      color: '#333',
      fonts: this.dfonts
    }
    if (this.db !== undefined) {
      v.b = this.db
    }
    if (this.di !== undefined) {
      v.i = this.di
    }
    if (this.dfont !== undefined) {
      v.font = this.dfont
    }
    if (this.dsize !== undefined) {
      v.size = this.dsize
    }
    if (this.dcolor !== undefined) {
      v.color = this.dcolor
    }
    return {
      showed: 'false',
      text: '',
      value: v
    }
  },
  props: [
    'dfont',
    'dsize',
    'di',
    'db',
    'dcolor',
    'dfonts'
  ],
  beforeMount () {
    let that = this
    this._close = e => {
      if (this.$el.contains(e.target)) {
        return
      }
      that.showed = 'false'
    }
    document.body.addEventListener('click', this._close)
  },
  beforeDestroy () {
    document.body.removeEventListener('click', this._close)
  },
  watch: {
    value (val) {
      this.$emit('onChange', this.value)
    }
  },
  methods: {
    displayShow () {
      this.showed = 'true'
    },
    displayHide () {
      this.showed = 'false'
    },
    displayDef () {
      this.showed = (this.showed === 'true' ? 'false' : 'true')
    },
    getText () {
      let v = ''
      if (this.value.b === 'true') {
        v += '粗 '
      }
      if (this.value.i === 'true') {
        v += '斜 '
      }
      v += this.value.size + ' '
      if (this.value.font.length > 15) {
        v += this.value.font.substring(0, 15) + '..'
      } else {
        v += this.value.font + ''
      }
      return v
    },
    ckb () {
      this.value.b = (this.value.b === 'true' ? 'false' : 'true')
      this.onChange()
    },
    cki () {
      this.value.i = (this.value.i === 'true' ? 'false' : 'true')
      this.onChange()
    },
    onChange () {
      this.$emit('onChange', this.value)
    }
  }
}
</script>

<style scoped>
  .tcolor{
    float: left;
    height: 15px;
    width: 15px;
    margin-right: 5px;
    margin-top: 10px;
    border:solid 1px #eee;
  }
  .def {
    height: 35px;
    font-size: 12px;
    line-height: 35px;
    text-align: center;
    padding: 0px 10px;
    cursor: pointer;
  }
  .set {
    padding: 20px;
    position:absolute;
    border:solid 1px #eee;
    background-color: #fff;
    margin-top: -1px;
    height: 200px;
    z-index: 9999;
    margin-left: 20px;
  }
  .tel{
    position:relative;
  }
  .bt{
    float: left;
    font-size: 12px;
    height: 30px;
    line-height: 30px;
    margin-right: 20px;
  }
  .s{
    color: #fff;
    background-color: #cccccc;
  }
  .n{
    color: #777;
    background-color: #ffffff;
  }
  .btn{
    width: 30px;
    height: 30px;
    border: solid 1px #eeeeee;
    float: left;
    margin-right: 20px;
    line-height: 30px;
    text-align: center;
    cursor: pointer;
    box-sizing: border-box;
  }
  .btn2{
    float: left;
    margin-right: 20px;
    margin-top: 8px;
  }
  .btn:hover{
    background-color: #eeeeee;
  }
  .btnck{
    background-color: #eeeeee;
  }
  .l1{
    float: left;
    clear: both;
    height: 45px;
  }
  .select{
    width: 115px;
    height: 30px;
    border: solid 1px #eeeeee;
    border-radius: 3px;
    text-indent: 5px;
  }
  .select2{
    width: 70px;
    height: 20px;
    border: solid 1px #eeeeee;
    border-radius: 3px;
    top: -3px;
    text-indent: 5px;
    position: relative;
  }
</style>