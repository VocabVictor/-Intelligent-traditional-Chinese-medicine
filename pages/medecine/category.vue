<template>
	<view class="category-list">
		<view class="title_box">
			<text class="main_title">高发症状</text>
			<text class="subtitle">及早发现 及时治疗</text>
		</view>
		<view class="category" v-for="(row, index) in categoryList" :key="index" @tap="toCategory(row)">
			<view class="img">
				<image :src="row.img"></image>
			</view>
			<view class="text">{{ row.name }}</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				keyword: "",
				statusBarHeight: 0,
				categoryList: []
			}
		},
		methods: {
			getData() {
				var that = this
				uni.request({
					url: 'https://api.hzxwhzxw.asia/categoryList',
					success: (res) => {
						if(res.statusCode == 200)
							that.categoryList = res.data
					},
					fail: (res) => {
						console.log('get失败');
					}
				})
			}
		},
		created: function() {
			this.getData()
		}
	}
</script>

<style lang="scss" scoped>
	.title_box
	{
		width: 100vw;
		margin-left: 8vw;
		height: 18px;
		display: flex;
		padding-top:4vh;
		align-items: center;
	}
	.main_title{
		display: flex;
		align-items: center;
		font-size: 18px;
		font-weight: bold;
		padding-right: 10px;
	}
	.main_title::after
	{
		display: inline-block;
		position: relative;
		left: 10px;
		content: "";
		width:2px;
		height:20px;
		background-color: rgba(121,121,121,0.5);
	}
	.subtitle{
		color: rgb(121,121,121);
		padding-left: 10px;
		font-size: 16px;
	}
	.category-list {
		width: 100%;
		margin: 3vh 0;
		padding-bottom: 4vh;
		border-bottom: solid 2upx #f6f6f6;
		display: flex;
		justify-content: space-between;
		background-color: white;
		flex-wrap: wrap;
		border-radius: 8px;

		.category {
			width: 25%;
			margin-top: 4vh;
			display: flex;
			flex-wrap: wrap;

			.img {
				width: 100%;
				display: flex;
				justify-content: center;

				image {
					width: 9vw;
					height: 9vw;
				}
			}

			.text {
				margin-top: 16upx;
				width: 100%;
				display: flex;
				justify-content: center;
				font-size: 14px;
				color: #3c3c3c;
			}
		}
	}
</style>
