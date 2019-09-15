<template>
	<view class="content" @touchstart="touchstart" @touchend="touchend">
		<view class="type"><span>第{{question.id}}题-{{type}}</span><span>{{question.id}}/{{count}}</span></view>
		<p><span>[多选]</span>{{question.question}}</p>
		<ul :class="{active: isActive}">
			<li class="option" :class="[question.answer.indexOf('A') !== -1 ? 'green' : 'red', select_a == true ? 'gray' : 'black']" @click="select('A')">
				<i>A</i>
				<view class="option-text">{{question.optionA}}</view>
			</li>
			<li class="option" :class="[question.answer.indexOf('B') !== -1 ? 'green' : 'red', select_b == true ? 'gray' : 'black']" @click="select('B')">
				<i>B</i>
				<view class="option-text">{{question.optionB}}</view>
			</li>
			<li class="option" :class="[question.answer.indexOf('C') !== -1 ? 'green' : 'red', select_c == true ? 'gray' : 'black']" @click="select('C')">
				<i>C</i>
				<view class="option-text">{{question.optionC}}</view>
			</li>
			<li class="option" :class="[question.answer.indexOf('D') !== -1 ? 'green' : 'red', select_d == true ? 'gray' : 'black']" @click="select('D')">
				<i>D</i>
				<view class="option-text">{{question.optionD}}</view>
			</li>
		</ul>
		<button class="item" type="primary" @click="commit()">确定</button>
	</view>
</template>

<script>
	import question_data from '../multiple_choice.js'
	export default {
		data() {
			return {
				question_data: question_data,
				count: 0,
				type: '多选题',
				question: {},
				select_option: '',
				selected: false,
				startPoint: {},
				endPoint: {},
				page_index: 0,
				isActive: false,
				select_a: false,
				select_b: false,
				select_c: false,
				select_d: false,
			}
		},
		onLoad() {
			this.question = this.question_data[0]
			this.count = this.question_data.length
		},
		methods: {
			commit() {
				this.isActive = true
			},
			select(option) {
				// if (this.selected) return
				if (option !== this.question.answer) {
					switch (option) {
						case 'A':
							this.select_a = !this.select_a
							break
						case 'B':
							this.select_b = !this.select_b
							break
						case 'C':
							this.select_c = !this.select_c
							break
						case 'D':
							this.select_d = !this.select_d
							break
						default:
						    break
					}
				}
				this.selected = true
			},
			nextQuestion() {
				this.selected = false
				this.isActive = false
				this.status = 0
				this.page_index ++
				this.question = this.question_data[this.page_index]
				this.select_a = this.select_b = this.select_c = this.select_d = false
			},
			prevQuestion() {
				this.selected = false
				this.isActive = false
				this.page_index --
				this.question = this.question_data[this.page_index]
			},
			/**
			 * @name 开始滑动
			 */
			touchstart(e) {
				this.startPoint={
					pageX:e.pageX||e.changedTouches[0].pageX,
					pageY:e.pageY||e.changedTouches[0].pageY,
				}
			},
			
			/**
			 * @name 滑动结束
			 */
			touchend(e) {
				this.endPoint={
					pageX:e.mp.changedTouches[0].pageX,
					pageY:e.mp.changedTouches[0].pageY,
				}
				// 判断是左滑动还是右滑动 当横向位移大于10，纵向位移大于100，则判定为滑动事件
				var disX=this.endPoint.pageX-this.startPoint.pageX;//计算移动的位移差
				var disY=this.endPoint.pageY-this.startPoint.pageY;
				if(Math.abs(disX)>10||Math.abs(disY)>100){
					if(Math.abs(disX)>Math.abs(disY)){//判断是横向滑动还是纵向滑动
					    if(disX>10){
							this.prevQuestion()
					    };
					    if(disX<-10){
							this.nextQuestion()
					    };
					}
				}
			},
		}
	}
</script>

<style>
	.content {
		position: absolute;
		height: 100%;
		margin: 0 35upx;
		font-size: 32upx;
	}
	.type {
		margin: 20upx 0;
		font-size: 28upx;
	}
	.type span:last-child{
		float: right;
		right: 0upx;
	}
	.option:first-child {
		margin-top: 10px;
	}
	.option {
		min-height: 100upx;
	}
	.option i {
		font-style: normal;
		line-height: 32px;
		color: #4680fe;
		text-align: center;
		display: inline-block;
		border: 1px solid #4680fe;
		height: 32px;
		width: 32px;
		margin: 0 10px 0 10px;
		float: left;
		border-radius: 25px;
	}
  .gray {
    color: #666666;
  }
  .gray i{
    color: #fff;
    background-color: #666666;
    border: 1px solid #666666;
  }
	.option-text {
		display: inline-block;
		width: 80%;
		height: 100%;
	}
	li {
		list-style: none;
	}
  .active .green i {
    color: #fff;
    background-color: #1AAD19;
    border: 1px solid #1AAD19;
  }
  .active .red.gray i {
    color: #fff;
    background-color: #FF3333;
    border: 1px solid #FF3333;
  }
	.active .green {
		color: #1AAD19;
	}
	.active .red.gray {
		color: #FF3333;
	}
</style>
