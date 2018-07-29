<template>
	<li  class="mx-option" v-show="display">
		<a href="javascript:void(0);" style="width:100%;text-align:left;border-bottom:1px #eee solid;" class="btn">{{label}}</a>
	</li>
</template>

<script>

export default {
	props:['value','label'],
	data:function(){
		return {
			display:true,
		}
	}
}

</script>