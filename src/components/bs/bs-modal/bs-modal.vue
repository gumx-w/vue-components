<template>
	<span @click="clickHander" v-show="display">
		<div class="modal fade in" tabindex="-1" style="display:block;" ref="modal">
			<div class="modal-dialog" :class="'modal-' + type" :style="{'width':width}">
				<div class="modal-content">
					<slot></slot>
				</div>
			</div>
		</div>
		<div class='modal-backdrop fade in' style="display:block;" ref="fade"></div>	
	</span>
</template>

<script>

export default {
	props:{
		type:{
			type:String,
			default:'md'
		},
		width:{
			type:String,
			default:null,
		}
	},
	data(){
		return {
			display:false,
		}
	},
	created(){
		this.$parent.$_bs_modal = {
			show:this.show,
			hide:this.hide,
			toggle:this.toggle,
		};
	},
	beforeDestroy(){
		this.$parent.$_bs_modal = null;
	},
	computed:{
		style(){
			return {
				display:'block',
			}
		}
	},
	methods:{
		toggle(){
			this.display = !this.display;
			if (this.display = false) {
				this.$emit('bs-hide');
			}else{
				this.$emit('bs-show');
			}
		},
		show(){
			this.display = true;
			this.$emit('bs-show');
		},
		hide(){
			this.display = false;
			this.$emit('bs-hide');
		},
		clickHander(event){
			let srcEl = event.srcElement;
			let className = srcEl.className;
			if (className == 'modal-backdrop fade in' || className == "modal fade in" || className.indexOf("modal-dialog") > -1 ) {
				this.hide();
				return;
			}
			let attr = srcEl.attributes['data-dismiss'] ;
			if (attr && attr.nodeValue == "modal") {
				this.hide();
				return;
			}
		},
	}
}

</script>