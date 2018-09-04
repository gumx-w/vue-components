<template>
	<div class="row" >
		<div class="form-group col-12">
			<h3>Tooltip</h3>
			 <div class="form-control" style="height: auto;">
				<div class="bs-example tooltip-demo">
					<div class="bs-example-tooltips" ref="btnGroup">
						<button type="button" class="btn btn-default" data-toggle="tooltip" data-placement="left" title="" data-original-title="Tooltip on left">Tooltip on left</button>
						<button type="button" class="btn btn-default" data-toggle="tooltip" data-placement="top" title="" data-original-title="Tooltip on top">Tooltip on top</button>
						<button type="button" class="btn btn-default" data-toggle="tooltip" data-placement="bottom" title="" data-original-title="Tooltip on bottom">Tooltip on bottom</button>
						<button type="button" class="btn btn-default" data-toggle="tooltip" data-placement="right" title="" data-original-title="Tooltip on right">Tooltip on right</button>
					</div>

					<bs-tooltip ref="tooltip"/>
				</div>
			 </div>
		</div>
	</div>
</template>

<script>
import BsTooltip from "../../components/bs/bs-tooltip"

export default {
	components:{BsTooltip},
	mounted(){
		this.$refs.tooltip.bind($(this.$refs.btnGroup).find("button"));
	}
}

</script>