<template>
  <div id="app" class="container">

    <div class="row" >
      <btn-group class="btn-group" v-model="selectBtn" :cancel="true" :multiselect="true">
        <btn-item value="A" label="A选项"/>
        <btn-item value="B" label="B选项"/>
        <btn-item value="C" label="C选项"/>
      </btn-group>
        
    </div>

    <div class="row text-left">
      <mark>
        基于 bootstrap 的多功能按钮组的实现，具有 单选、多选、反选 功能。</br>
        基于开放封闭原则的设计，可以在不修改 btn-group 组件的前提下，扩展更多的 btn-item。</br>
        只需要在实现新的 btn-item 时保证具有 value、label属性，并且 btn-item 的跟标签具有 mx-btn-item 样式就可以了。
      </mark>
    </div>


    <div class="row">
      <mx-select style="width:180px;height:40px;">
        <mx-option label="A选项"/>
        <mx-option label="B选项"/>
        <mx-option label="C选项"/>
        <mx-option label="D选项"/>
      </mx-select>

    </div>
    
    <div class="row text-left">
      <mark>
       多功能选择框：可单选选择、可搜索、可输入.
      </mark>
    </div>

  </div>
</template>

<script>

import {BtnGroup,BtnItem} from "./components/btnGroup"
import {MxSelect,MxOption} from "./components/mxSelect"

/**
 * 配合 boot
 */
export default {
  components:{
    BtnGroup,
    BtnItem,
    MxSelect,
    MxOption
  },
  name: 'app',
  data () {
    return {
      selectBtn:['A'],
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.row {margin-top: 10px;}



</style>
