<template>
  <div class="tel">
   <div v-if="lr === 'lb'" class='dsum-lr'>
     <div class="m-lr">
      <div class='dsum-title-b' :style='fontc'>{{dtitle}}</div>
      <div class='dsum-value-b' :style='fontb'>{{dvalue}}</div>
       </div>
   </div>
   <div v-if="lr === 'lt'" class='dsum-lr'>
     <div class="m-lr">
      <div class='dsum-value-t' :style='fontb'>{{dvalue}}</div>
      <div class='dsum-title-t' :style='fontc'>{{dtitle}}</div>
      </div>
   </div>
   <div v-if="lr === 'll'" class='dsum-lr'>
      <div class="m-lr">
      <div class='dsum-value-l' :style='fontb'>{{dvalue}}</div>
      <div class='dsum-title-l' :style='fontc'>{{dtitle}}</div>
      </div>
   </div>
   <div v-if="lr === 'lr'" class='dsum-lr'>
     <div class="m-lr">
      <div class='dsum-title-r' :style='fontc'>{{dtitle}}</div>
      <div class='dsum-value-r' :style='fontb'>{{dvalue}}</div>
     </div>
   </div>
  </div>
</template>

<script>
export default {
  name: 'dmSum',
  data () {
    return {
      title: this.dtitle,
      value: this.dvalue
    }
  },
  props: ['dtitle', 'dvalue', 'fontc', 'fontb', 'lr'],
  mounted () {
  },
  methods: {
  }
}
</script>

<style scoped>
.dsum {
  height:100%;
  width:100%;
}
.dsum-lr {
  height:100%;
  width:100%;
  display: flex;
  justify-content:center;
  align-items:center;
}

.dsum-title-b{
  clear: both;
  text-align: center; 
}
.dsum-value-b{
  clear: both;
  text-align: center; 
  position: relative;
  top:10px;
}
.dsum-title-t{
  clear: both;
  text-align: center; 
  position: relative;
  top:10px;
}
.dsum-value-t{
  clear: both;
  text-align: center; 
}
.dsum-title-l{
  height:100%;
  display: table-cell;
  vertical-align: middle;
  text-align: center; 
  position: relative;
  left: 10px; 
}
.dsum-value-l{
  height:100%;
  display: table-cell;
  vertical-align: middle;
  text-align: center;  
}
.m-lr {
  display: table;  
}
.dsum-title-r{
  height:100%;
  display: table-cell;
  vertical-align: middle;
  text-align: center;  
}
.dsum-value-r{
  height:100%;
  display: table-cell;
  vertical-align: middle;
  text-align: center;  
  position: relative;
  left: 10px;
}
  .tel{
    height:100%;
    width:100%;
  }
</style>