<template>
	<button type="button" class="mx-btn-item btn btn-primary " style="margin-right:10px;" :class="{'btn-success':active}">{{label}}</button>
</template>

<script>

export default {
	props:['value','label'],
	data:function(){
		return {
			'active':false,
		}
	}
}

</script>	