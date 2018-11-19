<template>
  <div class="tel">
    <span class="title">{{lineTitle}}</span>
    <table cellspacing="0" cellpadding="0">
      <thead>
      <tr>
        <th class="heard" v-for="(o, index2) in cols" v-bind:key="index2" @mouseover="overthistr(index2)" @mouseout="outthistr(index2)">
          <input type="text" v-model="cols[index2]" class="dmti_heard"/>
           <dmBtns ds="del" v-if="showstr[index2] === true" @click.native="clearvaluetr(index2)" class="btndel2"></dmBtns>
        </th>
        <th class="heard">
          <dmBtns ds="add" @click.native="addheard()" class="btndel"></dmBtns>
        </th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="(item, index1) in datas" v-bind:key="index1" class="line" @mouseover="overthis(index1)" @mouseout="outthis(index1)">
        <td v-for="(o, index2) in item.tr" v-bind:key="index2">
          <input type="text" v-model="item.tr[index2]" class="dmti_value"/>
        </td>
        <td>
          <dmBtns ds="del" v-if="shows[index1] === true" @click.native="clearvalue(index1)" class="btndel"></dmBtns>
        </td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'dmTable',
  data () {
    if (this.ddatas === undefined) {
      return {
        lineColor: this.dcolor,
        lineTitle: this.dtitle,
        show_del: false,
        shows: [],
        showstr: [],
        datas: [],
        cols: []
      }
    } else {
      return {
        lineColor: this.dcolor,
        lineTitle: this.dtitle,
        show_del: false,
        shows: [],
        showstr: [],
        datas: this.ddatas,
        cols: this.dcols
      }
    }
  },
  props: ['dcolor', 'dtitle', 'ddatas', 'dcols'],
  mounted () {
    let that = this
    this.datas.forEach(function (c) {
      that.shows.push(false)
      console.log('table show ')
    })
  },
  methods: {
    addheard () {
      this.cols.push('')
      this.datas.forEach(function (c) {
        c.tr.push('')
      })
      this.$emit('addheard')
    },
    borderColor (val) {
      return '#' + this.lineColor
    },
    clearvalue (index) {
      this.datas.splice(index, 1)
      this.shows.splice(index, 1)
    },
    clearvaluetr (index) {
      this.datas.forEach(function (c) {
        c.tr.splice(index, 1)
      })
      this.cols.splice(index, 1)
    },
    onChange (v) {
      console.log(this.datas)
    },
    bind (data) {
      let that = this
      data.forEach(function (c) {
        console.log(c)
        let one = c
        that.datas.push(one)
        that.shows.push(false)
      })
    },
    overthis (index) {
      this.shows.splice(index, 1, true)
      console.log('table show true')
      // this.show_del = true
    },
    outthis (index) {
      this.shows.splice(index, 1, false)
      // this.show_del = false
    },
    overthistr (index) {
      this.showstr.splice(index, 1, true)
      console.log('table show true')
      // this.show_del = true
    },
    outthistr (index) {
      this.showstr.splice(index, 1, false)
      // this.show_del = false
    }
  }
}
</script>

<style scoped>
  .tel{
    height: 30px;
    position: relative;
  }
  .title{
    float: left;
    clear: both;
  }
  .line{
    width: 100%;
    clear: both;
  }
  .line td{
    padding: 5px 0px;
  }
  .line:hover{
  }
  .dmti_value{
    height: 30px;
    border: none;
    border-bottom: solid 1px #eeeeee;
    width: 80px;
    text-align: center;
    margin-right: 10px;
    padding: 0px 5px;
  }
  .dmti_heard{
    height: 30px;
    border: none;
    border-bottom: solid 1px #eeeeee;
    width: 80px;
    text-align: center;
    padding: 0px 5px;
  }
  .btndel{
    position: relative;
    right: 5px;
    margin-top: 0px;
    margin-left: 15px;
  }
  .btndel2{
    position: absolute;
    margin-top: -32px;
    margin-left: 80px;
  }
  .heard{
    /* background-color: #eeeeee; */
    height: 45px;
    line-height: 45px;
  }
</style>