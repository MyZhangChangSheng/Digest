<template>
	<view>
		<cu-custom bgColor="bg-gradual-blue" :isBack="true">
			<block slot="backText">返回</block>
			<block slot="content">医学</block>
		</cu-custom>
		<scroll-view scroll-x class="bg-white nav text-center fixed" :style="[{top:CustomBar + 'px'}]">
			<view class="cu-item   titlename" :class="index==TabCur?'text-blue cur':''" v-for="(item,index) in tabNav"
				:key="index" @tap="tabSelect" :data-id="index">
				{{tabNav[index]}}
			</view>
		</scroll-view>
		<block v-if="TabCur==0">

			<view class="book">
				<view class="books" v-for="item in C_conduct" :key="item.C_conduct">
					<navigator :url="item.url">
						{{item.name}}
					</navigator>
				</view>
			</view>
		</block>
		<block v-if="TabCur==1">

			<view class="book">
				<view class="books" v-for="item in C_macroscopic" :key="item.C_macroscopic">
					<navigator :url="item.url">
						{{item.name}}
					</navigator>
				</view>
			</view>
		</block>

	</view>
</template>

<script>
	import database from "@/static/Database/database.js";
	export default {
		data() {
			return {
				C_macroscopic: database.C_macroscopic,
				C_conduct: database.C_conduct,
				CustomBar: this.CustomBar,
				TabCur: 0,
				// avatar:['https://ossweb-img.qq.com/images/lol/web201310/skin/big10001.jpg','https://ossweb-img.qq.com/images/lol/web201310/skin/big81005.jpg','https://ossweb-img.qq.com/images/lol/web201310/skin/big25002.jpg','https://ossweb-img.qq.com/images/lol/web201310/skin/big99008.jpg'],
				tabNav: ['中', '西', ],


			};
		},
		methods: {
			tabSelect(e) {
				this.TabCur = e.currentTarget.dataset.id;
				this.scrollLeft = (e.currentTarget.dataset.id - 1) * 60
			},
		}
	}
</script>

<style scoped>
	@import url("./../../static/Css/list.css");
</style>
