<template>
	<div class="question">
		<h2>{{question}}</h2>
	
		<div class="radioBox">
			<label v-for="item2 in option" :key="item2.value">
				<input type="radio" :name="'que'+index" :value="item2.value" @click='clickRadio(item2.value,index)'>{{item2.label}}
			</label>
		</div>
	</div>
</template>

<script>
export default {
	data(){
		return {
			option:[
				{label:'非常不同意',value:-3},
				{label:'不同意',value:-2},
				{label:'有点不同意',value:-1},
				{label:'中立',value:0},
				{label:'有点同意',value:1},
				{label:'同意',value:2},
				{label:'非常同意',value:3},
			],
			select:0,
		}
	},
	methods: {
		alertchild() {
			this.$emit('selectRadio')
		},
		up(){
			console.log('子组件选择了'+select)
		},
		clickRadio(v,i){
			this.select=v
			this.$emit('selectRadio',v,i)
		}
	},
	props:{
		index:Number,
		question: String
	}
}
</script>

<style>
</style>
