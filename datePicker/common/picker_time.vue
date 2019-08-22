<template>
	<view class="picker_time">
		<view class="pickers" v-if="visible">

			<view class="uni-mask"></view>
			<view class="time_picker">
				<view class="picker_list" :class="uni_picker_toggle">
					<view class="tab_bar">
						<view class="cancel" @tap="cancel()">{{cancelText}}</view>
						<view class="sure" style="color: #07bb07;" @tap="comfirm()">{{comfirmText}}</view>
					</view>
					<picker-view :indicator-style="indicatorStyle" :value="value" @change="bindChange">
						<picker-view-column>
							<view class="item" v-for="(item,index) in dateTime.years" :key="index">{{item}}年</view>
						</picker-view-column>
						<picker-view-column>
							<view class="item" v-for="(item,index) in dateTime.months" :key="index">{{item}}月</view>
						</picker-view-column>
						<picker-view-column>
							<view class="item" v-for="(item,index) in dateTime.days" :key="index">{{item}}日</view>
						</picker-view-column>
						<picker-view-column>
							<view class="item" v-for="(item,index) in dateTime.times" :key="index">{{item}}时</view>
						</picker-view-column>
						<picker-view-column>
							<view class="item" v-for="(item,index) in dateTime.minutes" :key="index">{{item}}分</view>
						</picker-view-column>
					</picker-view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'picker_time',
		data() {
			return{
			dateTime: {},
			uni_picker_toggle:'',
			indicatorStyle:`height: ${Math.round(uni.getSystemInfoSync().screenWidth/(750/100))}px;`
			}
		},
		props: {
			mode:{
				type: String,
				default: 'dateTime'
			},
			cancelText: {
				type: String,
				default: '取消'
			},
			comfirmText: {
				type: String,
				default: '确定'
			},
			startDate: {
				type: [String, Number],
				default: '1970'
			},
			endDate: {
				type: [String, Number],
				default: '2050'
			}
		},
		watch:{
			mode(){
				this.initData();
			}
		},
		methods: {
			forMatNum(num) {
				//规范格式
				const forMatNum = (num) => {
					return num < 10 ? '0' + num : num + '';
				}
			},
			initDate() {
				//初始化数据
				const date = new Date()
				const year = date.getFullYear()
				const endyear = year + 3;
				const month = date.getMonth() + 1
				const day = date.getDate()
				const time = date.getHours()
				const minute = date.getMinutes()
				for (let i = 1970; i <= year; i++) {
					dateTime.years.push(i)
				}
				for (let i = 1; i <= 12; i++) {
					dateTime.months.push(forMatNum(i))
				}
				for (let i = 1; i <= 31; i++) {
					dateTime.days.push(forMatNum(i))
				}
				for (var i = 0; i < 24; i++) {
					dateTime.times.push(forMatNum(i))
				}
				for (var i = 0; i < 60; i++) {
					dateTime.minutes.push(forMatNum(i))
				}
			},
			cancel() {
				//进入取消
			},
			comfirm() {
				//进入确定
			},
			bindChange(e) {

			}
		}

	}
</script>

<style>
	@import 'picker_time.css';
</style>
