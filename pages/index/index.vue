<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view>
			<text class="title">{{title}}</text>
			<navigator url="/pages/question/question" hover-class="navigator-hover">
				<button class="item" type="primary">{{item1}}</button>
			</navigator>
			
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'HJ刷题助手',
				item1: 'XX题库',
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style>
	.content {
		text-align: center;
		height: 400upx;
	}

	.logo {
		height: 200upx;
		width: 200upx;
		margin-top: 200upx;
	}

	.title {
		font-size: 36upx;
		color: #8f8f94;
	}
	
	.item {
		width: 300upx;
	}
</style>
