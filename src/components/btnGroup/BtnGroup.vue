<template>
	<div class="btn-group"  @click.prevent="click($event)"><slot></slot></div>
</template>

<script>

/**
 * 基于 bootstrap 的多功能按钮组的实现，具有 单选、多选、反选 功能。
 *
 * 基于开放封闭原则的设计，可以在不修改 btn-group 组件的前提下，扩展更多的 btn-item。
 * 只需要在实现新的 btn-item 时保证具有 value、label属性，并且 btn-item 的跟标签具有 mx-btn-item 样式就可以了。
 *
 */

export default {
	props:{
		value:{
			required:false
		},
		multiselect:{//是否可以多选
			required:false,
			default:false},
		cancel:{//是否可以反选
			required:false,
			default:false
		},
	},
	watch:{
		value:function(){
			this.updateActive();
		},
	},
	mounted:function(){
		if (this.multiselect == true) {
			if (!(this.value instanceof  Array)) {
				alert("多选模式下，value 值必须为数组！");
				return;
			}
		}
		this.updateActive();
	},
	updated:function(){
		this.updateActive();
	},
	methods:{
		click:function(event){
			let el = event.srcElement;
			if (el == this.$el) {
				return;
			}

			while(el.className.indexOf('mx-btn-item') == -1){
				el = el.parentElement;
			}

			let btns = this.$children;
			let selectValue = null;
			for(let btn of btns){
				if (el == btn.$el) {
					selectValue = btn.value;
					break;
				}
			}
			if (!this.multiselect) {//单选
				if (this.cancel == true) {//反选
					if (selectValue == this.value) {
						selectValue = null;
					}
				}
				this.$emit('input',selectValue);
				setTimeout(()=>{
					//延迟调用，解决父组件 watch异步的问题。
					this.$emit("select",selectValue);
				},300);
			}else{//多选
				let ov = this.value;
				if (ov) {
					let idx = ov.indexOf(selectValue);
					if (idx > -1) {
						ov.splice(idx,1)
					}else{
						ov.push(selectValue);
					}
					
				}
			}

		},
		updateActive:function(){
			let val = this.value;

			if (val === undefined) {
				return;
			}

			let multiselect = this.multiselect;
			let btns = this.$children;
			for(let btn of btns){
				if (!multiselect) {
					if (val == btn.value) {
						btn.active = true;
					}else{
						btn.active = false;
					}
				}else{
					if (val.indexOf(btn.value) > -1) {
						btn.active = true;
					}else{
						btn.active = false;
					}
				}
			}
		}

	}
}

</script>	