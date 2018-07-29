<template>
	<div style="position:relative;">
		<input  style="width:100%;height:100%;padding-left:5px;" type="text" 
		v-model="inputVal" 
		:placeholder="placeholder"  
		@blur="blur()"  
		@focus="showOptions = true;reloadOptions('');">
		
		<ul class="dropdown-menu"  style="overflow-x: hidden;max-height: 300px;width:100%;"  
		@click="selectOption($event)"
		:style="{'display':showOptions?'block':'none'}">
			<li v-show="!hasOption">未查询到数据</li>
			<slot></slot>
		</ul>
	</div>
</template>

<script>

/**
 * 多功能选择框：可单选选择、可多选、可搜索、可输入、
 */

export default {
	props:{
		value:{},
		width:{
			type:String,
			default:'100%',
		},
		height:{
			type:String,
			default:'100%',
		},
		editable:{
			type:Boolean,
			default:false,
		},
		placeholder:{
			default:'',
		}		
	},
	data:function(){
		return{
			inputVal:'',
			selectVal:null,
			showOptions:false,
			hasOption:false,
		}
	},
	mounted:function(){
		this.hasOption = this.$children.length > 0 ? true : false;
	},
	watch:{
		value:function(nv){
			setTimeout(()=>{
				for(let op of this.$children){
					if (op.value == nv) {
						this.inputVal = op.label;
					}
				}
			},100)
		},
		inputVal:function(nv){
			this.reloadOptions(nv);
			if (this.editable) {
				this.setSelectVal(nv);
			}
		}
	},
	methods:{
		setSelectVal:function(nv){
			this.$emit('input',nv);
			this.$emit('change',nv);
		},
		blur:function(){
			setTimeout(()=>{
				this.showOptions = false;
			},200);
		},
		reloadOptions:function(val){
			this.hasOption = false;
			for(let op of this.$children){
				let des = op.label;
				if (des && des.indexOf(val) > -1) {
					op.display = true;
					this.hasOption = true;
				}else{
					op.display = false;
					
				}
			}
		},
		selectOption:function(event){
			if (!this.hasOption) {
				this.showOptions = false;
				return;
			}
			let el = event.srcElement;
			while(el.className.indexOf('mx-option') == -1){
				el = el.parentElement;
			}
			
			let selectOp = null;
			for(let op of this.$children){
				if (op.$el == el) {
					selectOp = op;
				}
			}
			
			if (selectOp != null) {
				this.selectVal = selectOp.value;
				this.inputVal = selectOp.label;
			}

			this.setSelectVal(this.selectVal);
			this.showOptions = false;
		}
	}
}

</script>	