<template>
	<span class="mx-btn-item"  >
		<input type="radio" ref="input"/>
		<label>{{label}}</label>
	</span>
</template>

<script>

export default {
	props:['idx','value','label'],
	data:function(){
		return {
			'active':false,
		}
	},
	watch:{
		active:function(nv){
			if (nv == true) {
				this.$refs.input.checked = true;
			}else{
				this.$refs.input.checked = false;
			}
		}
	}
}

</script>	