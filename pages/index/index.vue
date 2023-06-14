<template>
	<view>
		<view id="pdfDom" style="padding-top: 15rpx;display: flex;width: 100vw;flex-wrap: wrap;padding-left: 40rpx;">
      <block v-if="txt">
        <view style="margin-left: 5rpx;height: 70rpx;"  v-for="(item,index) in txt" :key="index">
          <view style="border: 1px solid #4065F6;width: 80rpx;height: 10rpx;"></view>
          <view style="border: 1px solid #4065F6;width: 80rpx;height: 10rpx;border-top: none;"></view>
          <view style="border: 1px solid #4065F6;width: 80rpx;height: 10rpx;border-top: none;"></view>
          <view style="border: 1px solid #4065F6;width: 80rpx;height: 20rpx;border-top: none;font-size: 20rpx;display: flex;justify-content: center;align-items: center;">{{item}}</view>
        </view>
      </block>
      <block v-else>
        <view style="margin-left: 5rpx;height: 70rpx;"  v-for="(item,index) in txtInit" :key="index">
          <view style="border: 1px solid #4065F6;width: 80rpx;height: 10rpx;"></view>
          <view style="border: 1px solid #4065F6;width: 80rpx;height: 10rpx;border-top: none;"></view>
          <view style="border: 1px solid #4065F6;width: 80rpx;height: 10rpx;border-top: none;"></view>
          <view style="border: 1px solid #4065F6;width: 80rpx;height: 20rpx;border-top: none;font-size: 20rpx;display: flex;justify-content: center;align-items: center;">{{item}}</view>
        </view>
      </block>
		</view>
		<view style="border: 1px solid black;margin: 10rpx 20rpx;border-radius: 5rpx;font-size: 18rpx;letter-spacing: 20rpx;padding: 0rpx 10rpx;font-weight: 600;">
			<textarea style="width: 100%" v-model="txt" auto-height :maxlength="128" placeholder="输入打印的内容-限定128字符"/>
		</view>
    <view style="display: flex;padding: 20rpx;">
      <button @click="strUpset()" style="background: #e74c3c;color: white;">随机打乱</button>
      <button @click="generatePDF()" style="background: #007aff;color: white;">生成PDF</button>
    </view>
    <block v-if="!txt">
      <view style="display: flex;justify-content: center;height:100vh;align-items: center">
        <button @click="jump" style="background: #007aff;color: white;">跳转至拼音练习</button>
      </view>
    </block>

	</view>
</template>

<script>

	export default {
		data() {
			return {
				txt:'',
				htmlTitle: '生字注音练习册',
        txtInit:'打印内容不超过128位小于0位输入内容后自动清空'
			}
		},
		onLoad() {

		},
		methods: {
      generatePDF(){
        if(this.txt.length <= 128 && this.txt.length> 0){
          this.getPdf()
        }else{
          uni.showToast({
            title: '一张A4纸打印的字符不超过128位字符，不小于0位',
            icon:'none',
            duration: 2000
          });
        }
      },
      //字符串打乱方法
      shuffleString(str) {
        var shuffledString = '';
        str = str.split('');
        while (str.length > 0) {
          shuffledString += str.splice(Math.floor(Math.random() * str.length), 1);
        }
        return shuffledString;
      },
      strUpset(){
        if(this.txt.length> 0 && this.txt.length <= 128){
           let newStr = this.shuffleString(this.txt)
          this.txt = newStr
        }else{
          uni.showToast({
            title: '打乱内容不能为空哦',
            icon:'none',
            duration: 2000
          });
        }
      },
      //跳转
      jump(){
        uni.navigateTo({
          url: '/pages/PYIndex/index'
        });
      }
    }
	}
</script>

<style scoped>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
