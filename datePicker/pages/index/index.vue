<template>
	<view>
		<picker-time mode="dateTime" cancelText="取消" comfirmText="确定" startDate="1970" endDate="2050" ></picker-time>
	</view>
</template>

<script>
	import PickerTime from '@/common/picker_time.vue';
	export default {
		components: {
			PickerTime
		},
		data() {
			const date = new Date()
			const years = []
			const year = date.getFullYear()
			const endyear = year + 3;
			const months = []
			const month = date.getMonth() + 1
			const days = []
			const day = date.getDate()
			const times = []
			const time = date.getHours()
			const minutes = []
			const minute = date.getMinutes();
			for (let i = 1990; i <= endyear; i++) {
				years.push(i)
			}
			for (let i = 1; i <= 12; i++) {
				months.push(i)
			}
			for (let i = 1; i <= 31; i++) {
				days.push(i)
			}
			for (var i = 0; i < 24; i++) {
				times.push(i)
			}
			for (var i = 0; i < 60; i++) {
				minutes.push(i)
			}
			return {
				years,
				year,
				months,
				month,
				days,
				day,
				times,
				time,
				minutes,
				minute,
				date: '',
				uni_picker_toggle: '',
				value: [year - 1990, month - 1, day - 1, time, minute],
				visible: false,
				indicatorStyle: `height: ${Math.round(uni.getSystemInfoSync().screenWidth/(750/100))}px;`
			}
		},
		onLoad() {
			this.date = this.year + "-" + this.month + "-" + this.day + '-' + " " + this.time + ":" + this.minute;
		},
		methods: {
			isShow() {
				this.visible = !this.visible;
			},
			bindChange(e) {
				const val = e.detail.value
				this.year = this.years[val[0]]
				this.month = this.months[val[1]]
				this.day = this.days[val[2]]
				this.time = this.times[val[3]]
				this.minute = this.minutes[val[4]]
			},
			getTime() {
				this.date = this.year + "-" + this.month + "-" + this.day + '-' + " " + this.time + ":" + this.minute;
				this.visible = !this.visible;
			}

		}
	}
</script>
