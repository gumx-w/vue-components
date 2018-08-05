<template>
	<li class="mx-option" v-show="display">{{label}}</li>
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