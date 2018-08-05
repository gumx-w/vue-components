<template>
<div class="row" >
    <div class="form-group col-12">
        <h5>BtnGroup 按钮组</h5>
        <p class="text-muted">
            基于 bootstrap 的多功能按钮组的实现，具有 单选、多选、反选 功能。</br>
            基于开放封闭原则的设计，可以在不修改 btn-group 组件的前提下，扩展更多的 btn-item 类型。</br>
            <mark>只需要在实现新的 btn-item 时保证具有 value、label属性，并且 btn-item 的跟标签的 class 有 mx-btn-item 就可以了。</mark>
        </p>
        <div class="form-control" style="height: auto;">
            <div class="form-group">
                <label class="control-label">单选</label>
                <div class="col-12">
                    <btn-group class="btn-group" v-model="value1">
                        <btn-item value="A" label="A选项"/>
                        <btn-item value="B" label="B选项"/>
                        <btn-item value="C" label="C选项"/>
                    </btn-group>
                </div>

            </div>

            <div class="form-group">
                <label class="control-label">多选选</label>
                <div class="col-12">
                    <btn-group class="btn-group" v-model="value2" :multiselect="true">
                        <btn-item value="A" label="A选项"/>
                        <btn-item value="B" label="B选项"/>
                        <btn-item value="C" label="C选项"/>
                    </btn-group>
                </div>
            </div>

            <div class="form-group">
                <label class="control-label">可反选</label>
                <div class="col-12">
                    <btn-group class="btn-group" v-model="value3" :cancel="true">
                        <btn-item value="A" label="A选项"/>
                        <btn-item value="B" label="B选项"/>
                        <btn-item value="C" label="C选项"/>
                    </btn-group>
                </div>
            </div>
        </div>        
    </div>
</div>
</template>

<script type="text/javascript">
import {BtnGroup,BtnItem} from "../components/btnGroup"


export default{
	components:{BtnGroup,BtnItem},
	data:function(){
		return{
			value1:'A',
			value2:['A','B'],
			value3:'A',
		}
	}
}
</script>