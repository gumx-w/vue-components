<template>
	<div class="tooltip fade in" :class="direction" :style="style" role="tooltip">
      <div class="tooltip-arrow"></div>
      <div class="tooltip-inner" ref="msg">tooltip</div>
    </div>
</template>

<script>

export default {
	data(){
		return{
			top:0,
			left:0,
			display:true,
			direction:'left',
		}
	},
	computed:{
		style(){
			return{
				left:this.left + 'px',
				top:this.top + 'px',
				opacity:this.display ? 1 : 0,
			}
		}
	},
	methods:{
		bind(els){
			for (var i = 0; i < els.length; i++) {
				let e = els[i];
				e.addEventListener('mouseenter',this.show);
				e.addEventListener('mouseleave',this.hide);
			}
		},
		unbind(els){
			for (var i = 0; i < els.length; i++) {
				let e = els[i];
				e.removeEventListener('mouseenter',this.show);
				e.removeEventListener('mouseleave',this.hide);
			}
		},
		show($event){
			console.log($event.currentTarget);
			let e = $event.currentTarget;
			let msg = e.attributes['data-placement'].nodeValue;
			let direction = e.attributes['data-placement'].nodeValue;
			if (!msg) {
				return;
			}


			let offsetTop = e.offsetTop; 
			let offsetLeft =e.offsetLeft; 
			let offsetParent = e.offsetParent;
			while(offsetParent != null){
				offsetTop += offsetParent.offsetTop;
				offsetLeft += offsetParent.offsetLeft;
				offsetParent = offsetParent.offsetParent;
			}
			
			this.$refs.msg.innerText = msg;
			let eW = e.scrollWidth;
			let eH = e.scrollHeight;
			let msgW = this.$refs.msg.scrollWidth + 8;
			let msgH = this.$refs.msg.scrollHeight;
			if (direction == 'left') {
				offsetLeft -= msgW;
				offsetTop += (eH - msgH) /2
			}else if(direction == 'right'){
				offsetLeft += e.scrollWidth;
				offsetTop += (eH - msgH) /2
			}else if(direction == 'top'){
				offsetTop -= (msgH + 8);
				offsetLeft += (eW- msgW) / 2
			}else if(direction == 'bottom'){
				offsetTop += e.scrollHeight;
				offsetLeft += (eW- msgW) / 2
			}



			this.top = offsetTop;
			this.left = offsetLeft;
			this.display = true;
			this.direction = direction;
		},
		hide($event){
			this.display = false;
		}
	}
}

</script>