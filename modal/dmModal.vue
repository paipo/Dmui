<template> 
  <div class="modal-backdrop" @click="close" v-show="show"> 
    <div class="modal" @click.stop :style="{height:h + 'px',width:w + 'px'}"> 
      <div class="modal-header"> 
        <slot name="header"> 
          <h2>this is title</h2>
        </slot> 
        <button type="button" class="btn-close" @click="close">x</button> 
      </div> 
      <div class="modal-body"> 
        <slot name="body">this is body</slot> 
      </div> 
      <div class="modal-footer" v-show="dshowbottom"> 
        <slot name="footer">this is bottom<button type="button" class="btn-green" @click="close">关闭</button></slot>
      </div> 
    </div> 
  </div> 
</template> 
<script>
export default {
  name: 'dmModal',
  data () {
    return {
      dshow: this.show,
      dshowbottom: this.showbottom
    }
  },
  props: [
    'showbottom',
    'show',
    'w',
    'h'],
  methods: {
    close: function () {
      this.dshow = false
      this.$emit('close')
    }
  }
}
</script> 
<style scoped> 
.modal-backdrop { 
  position: fixed; 
  top: 0; 
  right: 0; 
  bottom: 0; 
  left: 0; 
  background-color: rgba(109, 107, 107, 0.3); 
  display: flex; 
  justify-content: center; 
  align-items: center; 
  z-index: 9999999;
} 
.modal { 
  background-color: #fff; 
  box-shadow: 2px 2px 20px 1px #999999; 
  overflow-x:auto; 
  display: flex; 
  flex-direction: column; 
  z-index: 1000000;
} 
.modal-header, .modal-footer { 
  padding: 15px; 
  display: flex; 
} 
.modal-header { 
  border-bottom: 1px solid #eee; 
  color: #4aae9b; 
  justify-content: space-between; 
} 
.modal-footer { 
  border-top: 1px solid #eee; 
  justify-content: flex-end; 
} 
.modal-body { 
  position: relative; 
  padding: 20px 10px; 
} 
.btn-close { 
  border: none 0; 
  font-size: 20px; 
  padding: 0px; 
  cursor: pointer; 
  font-weight: bold; 
  color: #4aae9b; 
  background-color: transparent; 
  position: relative;
  margin-top: -20px;
} 
.btn-green { 
  color: #fff; 
  background-color: #4aae9b; 
  border: 1px solid #4aae9b; 
  border-radius: 2px; 
} 
</style>
