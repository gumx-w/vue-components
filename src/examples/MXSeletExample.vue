<template>
<div class="row" >
    <div class="form-group col-12">
        <h5>MXSelect 下拉选择</h5>
        <p class="text-muted" >
            <p>多功能的下拉选择框：输入、选择、筛选。</p>
            <p>  该组件响应两个值： 
                    1. 输入的字串值 input-value
                    2. 选择的结果值 select-value</p>

            <p>  父组件到子组件方向： 
                    1. 传递到子组件的input值会只会影像到选择列表的匹配结果，不会影响到select-value。
                    2. 传递到子组件的 select 的值，会首先从可选择列表中寻找匹配项， 如果找到则会用匹配到的option的label字段覆盖 input-value，如果找不到则不做任何响应</p>

            <p>  子组件到父组件方向：
                    1. 当输入完毕，输入的值发生改变的时候，会将新值更新给父组件 input-value
                    2. 当选择某个值时，会将 option 的 value 更新给父组件的 select-value， 将 option 的label 更新给父组件的 input-value</p>
        </p>
        <div class="form-control">
            <div class="form-group">
                <label class="control-label">单选</label>
                <div class="col-4">
					<mx-select class="form-control"
                    :select-value="selectValue"
                    @update:select-value="selectValue = $event"
                    :input-value="inputValue"
                    @update:input-value="inputValue = $event">
						<mx-option value="A" label="A 选项"/>
                        <mx-option value="B" label="B 选项"/>
                        <mx-option value="C" label="C 选项"/>
                        <mx-option value="D" label="D 选项"/>
					</mx-select>
                </div>
                <br>
                <div class="col-4">
                    <div class="form-group">
                        <label>select-value：</label>
                        <input type="text" class="form-control" v-model="selectValue">
                    </div>
                </div>
                <div class="col-4">
                    <div class="form-group">
                        <label>select-value：</label>
                        <input type="text" class="form-control" v-model="inputValue">
                    </div>
                </div>                
            </div>
        </div>        
    </div>
</div>
</template>

<script type="text/javascript">
import {MxSelect,MxOption} from "../components/mxSelect"

export default{
	components:{MxSelect,MxOption},
    data:function(){
        return{
            selectValue:"A",
            inputValue:"A 选项",
        }
    }


}

</script>