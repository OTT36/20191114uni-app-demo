<template>
	<view>
        <view class="uni-padding-wrap uni-common-mt">
            <view class="uni-flex uni-row">
              <navigator url="/pages/question/single_choice/single_choice" hover-class="navigator-hover">
                <view class="uni-flex-item">
                  <uni-icon type="compose"></uni-icon>
                  <span class="text">单选题</span>
                </view>
              </navigator>
              <navigator url="/pages/question/multiple_choice/multiple_choice" hover-class="navigator-hover">
                <view class="uni-flex-item">
                  <uni-icon type="compose"></uni-icon>
                  <span class="text">多选题</span>
                </view>
              </navigator>
              <navigator url="/pages/question/judgment_choice/judgment_choice" hover-class="navigator-hover">
                <view class="uni-flex-item">
                  <uni-icon type="compose"></uni-icon>
                  <span class="text">判断题</span>
                </view>
              </navigator>
              <navigator url="/pages/question/case_choice/case_choice" hover-class="navigator-hover">
                <view class="uni-flex-item">
                  <uni-icon type="compose"></uni-icon>
                  <span class="text">案例题</span>
                </view>
              </navigator>
            </view>
        </view>
    </view>
</template>

<script>
	import uniIcon from "@/components/uni-icon/uni-icon.vue"  
	export default {
		data() {
			return {
				title: 'HJ刷题助手',
				item1: '题库1',
				question_data: ''
			}
		},
		onLoad() {
		},
		methods: {
		},
		components: {uniIcon}
	}
</script>

<style>
  .uni-flex {
    display: flex;
    justify-content: space-between;
  }
	.uni-flex-item {
		height: 250upx;
	}
	.text {
		display: block;
		text-align: center;
		font-size: 40upx;
	}
	.uni-icon-compose {
		font-size: 5em;
	}
</style>
