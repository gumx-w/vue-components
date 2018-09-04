<template>
<div class="row" >
    <div class="form-group col-12">
        <h3>模态框</h3>
        <p class="text-muted" >
        	<p>实现基础功能：</p>

			<ul>
				<li>this.$_bs_modal 绑定 modal 组件实例。 开放方法： show、hide、toggle</li>
				<li>@bs-hide 关闭事件回调</li>
				<li>@bs-show 打开事件回调</li>
			</ul>
        </p>
        <div class="form-control" style="height: auto;">
			<button type="button" class="btn btn-primary" @click="showModal">SHOW MODAL</button>
			<br><br>
			<p class="bg-info">状态：{{msg}}</p>
			<bs-modal ref="modal" @bs-hide="msg='隐藏'" @bs-show="msg='显示'">
				<div class="modal-dialog modal-sm" role="document">
					<div class="modal-content">
						<div class="modal-header">
							<button type="button" class="close" data-dismiss="modal" aria-label="Close">&times;</button>
							<h4 class="modal-title">Modal title</h4>
						</div>
						<div class="modal-body">
							<p>One fine body&hellip;</p>
						</div>
						<div class="modal-footer">
							<button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
							<button type="button" class="btn btn-primary">Save changes</button>
						</div>
					</div>
				</div>
			</bs-modal>
        </div>
    </div>
</div>

</template>

<script>

import BsModal from "../../components/bs/bs-modal"

export default {
	data(){
		return{
			msg:"隐藏"
		}
	},
	components:{
		BsModal,
	},
	mounted(){
		console.log(2);
	},
	methods:{
		showModal(){
			this.$_bs_modal.show();
		}
	}	
}

</script>