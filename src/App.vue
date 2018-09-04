<template>
<div id="app" class="container"><br>
    <btn-group-example /><br>
    <mx-select-example /><br>
    <bs-modal-example />
    <bs-dropdown-example />
</div>
</template>

<script>
import BtnGroupExample from "./examples/mx/BtnGroupExample.vue"
import MxSelectExample from "./examples/mx/MXSeletExample.vue"

import BsModalExample from "./examples/bs/bs-modal-example.vue"
import BsDropdownExample from "./examples/bs/bs-tooltip-example.vue"

export default {
  components:{
    BtnGroupExample,
    MxSelectExample,
    BsModalExample,
    BsDropdownExample
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

