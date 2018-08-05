<template>
<div id="app" class="container"><br>
    <btn-group-example /><br>
    <mx-select-example /><br>
</div>
</template>

<script>
import BtnGroupExample from "./examples/BtnGroupExample.vue"
import MxSelectExample from "./examples/MXSeletExample.vue"
export default {
  components:{
    BtnGroupExample,
    MxSelectExample
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

