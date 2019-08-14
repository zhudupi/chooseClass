<template>
  <div id="app">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App" v-for="(item,index) in questions" :key="index" :child="item"/>-->
	<template v-if='cur<30'>
	<div>第{{cur+1}}/30题</div>
	 <question v-for="(item,index) in questions" v-if="index==cur" :key="index" :index="index" :question="item" @selectRadio='selectRadio'/> 
	 
	 <a v-show="cur!=0" href="javascript:void(0)" @click="cur--">上一题</a>
	 <!-- <img src="./assets/img/nav1.png" alt=""> -->
	 </template>
	 <div v-else>
		 你适合你的学级是<br>
		 <template v-for="(pic,index) in result">
			<span v-if="index>0">或</span><img :src="pic" alt="">
		</template>
	 </div>
	 <!-- <template v-for="(pic,index) in imgurl">
	 	<span v-if="index>0">或</span><img :src="pic" alt="">
	 </template> -->
  </div>
</template>

<script>
import question from './components/question.vue'

export default {
  name: 'app',
  data() {
	  return {
		  cur: 0,
		  questions:['我在和别人交往的时候很看重智商','我比较希望自己的行为都在自己的控制之下','在做出决定之前，我会考虑到所有的可能性','天赋比努力更重要','我认为人不分阶级，应该被平等对待','当专注于兴趣时，我经常忘记时间','即使会伤害到别人，我也会选择坦诚','熟悉的环境比陌生的环境更让我感到舒适','我总喜欢拖延','休息时我更喜欢家里蹲，而不是户外活动','遇到令我困扰的事情，我喜欢逃避来维系内心的安宁','面临压力时我会保持冷静','即使最后是徒劳无功，我也会坚持完成我的想法直到实现','我依靠我的天赋学习','我喜欢被人关注','我会停下手头的事情去帮助有需要的人','我更喜欢独处而不是与人共处','我不惧挑战那些超出我能力的事情','有人会说我难以接近','我更像一只独狼，而不是交际花','我可以轻松的与任何人进行交谈','我更喜欢呆在远离底线的安全地带','我看待事物比较乐观','我更喜欢自学而不是去上课','我有让生活变轻松的方法','我内心其实非常在意自己的言行','我会尽量不让事情有变数','我总是被当成小孩子对待','当我做事时，我自己的利益优先于团队的利益','我喜欢满足自己的好奇心'],
		  answer:[[],[],[]],
		  result:false,
		  imgurl:[require('./assets/img/nav1.png'),require('./assets/img/nav2.png'),require('./assets/img/nav3.png')]
	  }
  },
  methods:{
	selectRadio(v,i){
		// if(this.cur<6){
		// 	
		// 		this.answer[Math.floor(i/2)][i-Math.floor(i/2)*2]=v;
		// }
			this.answer[Math.floor(i/10)][i-Math.floor(i/10)*10]=v;
		// if(this.answer[Math.floor(i/10)][i-Math.floor(i/10)*10]||this.answer[Math.floor(i/10)][i-Math.floor(i/10)*10]==0){
			this.cur++;
		// }
		if(this.cur>=this.questions.length){
			var that=this;
			console.log('答案计算中')
			// this.answer.forEach(function(e,i){
			// 	e.reduce(function(prev,cur){return prev+cur})
			// })
			var a=this.answer[0].reduce(function(prev,cur){return prev+cur});
			var b=this.answer[1].reduce(function(prev,cur){return prev+cur});
			var c=this.answer[2].reduce(function(prev,cur){return prev+cur});
			var max=Math.max.apply(Math,[a,b,c])
			var arr=[];
			[a,b,c].forEach(function(e,i){
				arr.push(that.imgurl[i]);
			})
			this.result=arr
		}
	},
	
  },
  components: {
    question
  }
}

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
