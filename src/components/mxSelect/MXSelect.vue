<template>
	<div style="position: relative;padding: 0px;">
		<input style="width:100%;height:100%;padding-left:5px;" type="text" 
		v-model="inputStr"  
		:placeholder="placeholder" 
		@blur="blur()"  
		@focus="focus()" 
		@change="inputValueChange()" />
		
		<ul class="dropdown-menu" style="overflow-x: hidden;max-height: 300px;width:100%;position: absolute;" 
		:style="{'display':showOption?'block':'none'}" 
		@click="selectOption($event)">
			<li v-show="!hasOption">未查询到数据</li>
			<slot></slot>
		</ul>
	</div>
</template>

<script>

export default {
	props:{
		selectValue:{},//选中的值
		inputValue:{},//输入的值
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
			inputStr:'',
			selectedOption:null,
			showOption:false,
			hasOption:false,
		}
	},
	watch:{
		selectValue:function(nv){
			this.reloadSelecteOption(nv);
		},
		inputStr:function(str){
			this.reloadOptions();
		},
		inputValue:function(nv){
			this.inputStr = nv;
		},
	},
	computed:{
		mxOptions:function(){
			let options = this.$children;
			return options;
		}
	},
	updated:function(){
		this.$nextTick(()=>{
			//对比 option 是否发生了变化
			//由于子组件更新导致的刷新selected Option ，此时如果 selected Option 已经更新了，就不不用再重复调用了
			let children = this.$children;
			let childrenUids = "";
			for(let c of children){
				childrenUids += "-" + c._uid;
			}
			if (this._oldChildUids != childrenUids) {
				this._oldChildUids = childrenUids;
				setTimeout(()=>{
					this.reloadSelecteOption(this.selectValue,true);
				},100)
			}
		});
	},
	mounted:function(){
		this.inputStr = this.inputValue;
	},
	methods:{
		inputValueChange:function(isFromOption){
			let str = this.inputStr;
			if (!isFromOption) {
				this.$emit('update:select-value',null);
			}
			this.$emit('update:input-value',str);
		},
		setSelectedOption:function(nv){
			this.selectedOption = nv;
			this.$emit('update:select-value',nv.value);
			if (nv != null) {
				this.inputStr = nv.label;
				this.inputValueChange(true);
			}
		},
		blur:function(){
			setTimeout(()=>{
				this.showOption = false;
			},200);
		},
		focus:function(){
			this.showOption = true;
			this.reloadOptions(true);
		},
		reloadSelecteOption:function(nv,isChildrenUpdate){
			//传进来的值是option中的value，
			let options = this.mxOptions;
			let selectOp;
			for(let o of options){
				if (nv == o.value) {
					if (isChildrenUpdate && o == this.selectedOption) {
						//由于子组件更新导致的刷新selected Option ，此时如果 selected Option 已经更新了，就不不用再重复调用了
						return;
					}
					this.setSelectedOption(o);
					break;
				}
			}
		},
		reloadOptions:function(showAll){
			let str = this.inputStr;
			//修改输入内容时，每一次input获取到焦点的时候，都需要刷新 options 的显示状态以及剩余显示个数
			this.hasOption = false;
			let options = this.mxOptions;
			for(let op of options){
				let des = op.label;
				if (showAll) {
					op.display = true;
					this.hasOption = true;
				}else{
					if (des && des.indexOf(str) > -1) {
						op.display = true;
						this.hasOption = true;
					}else{
						op.display = false;
					}
				}
			}
		},
		selectOption:function(event){
			
			//1. 找到点击的 option 元素，如果找不到就直接返回
			let targetElement = event.currentTarget;
			let el = event.srcElement;
			while(el.className.indexOf('mx-option') == -1 && el != targetElement){
				el = el.parentElement;
			}

			if (el == targetElement) {
				//说明没找到option，直接返回
				return;
			}

			this.showOption = false;
			//2. 根据选中的 元素，找到对应的vue对象
			let options = this.$children;
			for(let op of options){
				if (op.$el == el) {
					this.setSelectedOption(op);
					break;
				}
			}
		}
	}
}

</script>	