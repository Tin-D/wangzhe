<template>
	<div>
		<el-input v-model="clientHeight" placeholder=""></el-input>
		<S-wiper></S-wiper>
		<!-- end of swiper -->
		<Icons></Icons>
		<!-- end of nav icons -->

		<!-- <m-card title="新闻资讯">
          <div class="nav jc-between">
              <div class="nav-item active">
                <div class="nav-link">热门</div>
              </div>
              <div class="nav-item">
                <div class="nav-link">热门</div>
              </div>
              <div class="nav-item">
                <div class="nav-link">热门</div>
              </div>
              <div class="nav-item">
                <div class="nav-link">热门</div>
              </div>
              <div class="nav-item">
                <div class="nav-link">热门</div>
              </div>
            </div>
            <div class="pt-3">
              <swiper >
                <swiper-slide v-for="m in 5" :key="m">
                  <div class="py-2 d-flex" v-for="n in 5" :key="n">
                    <span>[新闻]</span>
                    <span>|</span>
                    <span class="flex-1">夏日是个别那么爱上对方会啊是覅</span>
                    <span>06/15</span>
                  </div>
                </swiper-slide>
              </swiper>
            </div>
		</m-card>-->

		<m-list-card icon="menu1" title="新闻资讯" :categroies="newsCats">
			<template #items="{ category, a }">
				<div
					class="py-2 d-flex"
					v-for="(news, i) in category.newsList"
					:key="i"
				>
					<span>[{{ news.categoryName }}]</span>
					<span>|</span>
					<span class="flex-1">{{ news.title }}</span>
					<span>{{ news.data }}</span>
				</div>
				<div
					class="py-2 d-flex"
					v-for="i in a"
					:key="i"
				>
					<span>{{i}}</span>
				</div>
			</template>
		</m-list-card>

		<Dc1></Dc1>

		<m-card title="英雄列表">
			<about>
				<inject :tableProxy="tableProxy"></inject>
			</about>
		</m-card>

		<!-- 
			.sync就是相当于父传子，子组件需要改动父组件的这个值
			-------------- 子 --------------
			<input @input="sendMsg" :value="title" />
			sendMsg (event) {
				this.$emit('updatetitle', event.target.value)
			}
			-------------- 父 --------------
			<text-document :title="doc.title" @updatetitle="doc.title = $event"></text-document>
			这时.sync相当于这个操作省去这个步骤 
		-->
		<m-card :title.sync="title">
			<template #cardSlot>
				<el-input v-model="title"></el-input>
			</template>
			<div>{{title}}</div>
		</m-card>

		<m-card title="图文攻略">图文攻略</m-card>

		<div>
			<h1 @click="goVex">vex案例</h1>

			<h1 @click="sideBar">侧边栏路由</h1>

			<h1 @click="childRouter">子路由</h1>

			<h1 @click="vueDirctives">veu各种指令</h1>

			<h1 @click="css">Css库</h1>

			<h1 @click="store">Store</h1>

			<h1 @click="state">State</h1>

			<h1 @click="getters">Getters</h1>

			<h1 @click="mutations">Mutations</h1>

			<h1 @click="actions">Actions</h1>

			<h1 @click="modules">Modules</h1>

			<h1 @click="router">Router</h1>

			<h1 @click="echarts">Echarts</h1>

			<h1 @click="canvas">canvas</h1>

			<h1 @click="Vueuse">Vueuse</h1>

			<h1 @click="elementUI">elementUI</h1>

			<h1 @click="search">search</h1>
			
		</div>
	</div>
</template>

<script>
import Axios from "axios";
import About from "@/views/About";
import Inject from "@/views/inject";

export default {
	components: { About, Inject },
	created() {
		console.log(this.$children);
		console.log(this.array);
	},
	events: {
		testEvent(testEvent) {
			console.log(testEvent);
		},
		fire(jieke) {
			console.log(jieke);
		},
	},
	data() {
		return {
			title: '精彩视频',
			array: new Array(100).keys(),
			clientHeight: null,
			tableProxy: {
				seq: true, // 启用动态序号代理
				props: {
					result: "resultsq12",
					total: "pageVO.sumTotal",
				},
				ajax: {
					// 任何支持 Promise API 的库都可以对接（fetch、jquery、axios、xe-ajax）
					query: (params) => this.godata(params),
				},
			},
			tableColumn: [
				{ type: "checkbox", width: 50 },
				{ type: "seq", width: 60 },
				{ field: "name", title: "Name" },
			],
			swiperOptions: {
				pagination: {
					el: ".pagination-home",
				},
			},
			tableData: new Array(1000).fill({}).map((a, index) => ({
				sex: index + 100,
				age: index,
				address:
					"自动跟随某个属性的变化去重新计算表格，和手动调用 recalculate 方法是一样的效果（对于通过某个属性来控制显示/隐藏切换时可能会用到）",
			})),
			newsCats: [
				{
					name: "热门",
					newsList: new Array(5).fill({}).map((v, index) => ({
						categoryName: "热门" + Number(index),
						title: "6yue2hao",
						data: "06/01",
					})),
				},
				{
					name: "新闻",
					newsList: new Array(5).fill({}).map((v, index) => ({
						categoryName: "新闻" + Number(index + 1),
						title: "6yue2hao",
						data: "06/01",
					})),
				},
				{
					name: "公告",
					newsList: new Array(5).fill({}).map((v, index) => ({
						categoryName: "公告" + Number(index + 1),
						title: "6yue2hao",
						data: "06/01",
					})),
				},
				{
					name: "活动",
					newsList: new Array(5).fill({}).map((v, index) => ({
						categoryName: "活动" + Number(index + 1),
						title: "6yue2hao",
						data: "06/01",
					})),
				},
				{
					name: "赛事",
					newsList: new Array(5).fill({}).map((v, index) => ({
						categoryName: "新闻" + Number(index + 1),
						title: "6yue2hao",
						data: "06/01",
					})),
				},
			],
		};
	},
	methods: {
		goVex() {
			this.$router.push("/goVex");
		},
		sideBar() {
			this.$router.push("/sideBar");
		},
		childRouter() {
			this.$router.push("/childRouter");
		},
		vueDirctives() {
			this.$router.push("/vueDirctives");
		},
		css() {
			this.$router.push("/css");
		},
		store() {
			this.$router.push("/store");
		},
		state() {
			this.$router.push("/state");
		},
		getters() {
			this.$router.push("/getters");
		},
		mutations() {
			this.$router.push("/mutations");
		},
		actions() {
			this.$router.push("/actions");
		},
		modules() {
			this.$router.push("/modules");
		},
		router() {
			this.$router.push("/router");
		},
		echarts() {
			this.$router.push("/echarts");
		},
		canvas() {
			this.$router.push("/canvas");
		},
		Vueuse() {
			this.$router.push("/Vueuse");
		},
		elementUI() {
			this.$router.push("/elementUI");
		},
		search() {
			this.$router.push("/search");
		},
		async godata(params) {
			const { data } = await Axios.get(`/api/brand_model`);
			const page = params.page;
			const startIndex = (page.currentPage - 1) * page.pageSize;
			var rest = {
				results: data.slice(startIndex, startIndex + page.pageSize),
				pageVO: {
					sumTotal: data.length,
				},
			};
			return rest;
		},
	},
	mounted() {
		this.clientHeight = document.body.clientHeight;
	},
};
</script>

<style lang="scss">
@import "@/assets/scss/var.scss";

.pagination-home {
	.swiper-pagination-bullet {
		opacity: 1;
		border-radius: 0.1538rem;
		background: map-get($colors, "white");

		&.swiper-pagination-bullet-active {
			background: map-get($colors, "button");
		}
	}
}

.nav-icons {
	border-top: 1px solid $border-color;
	border-bottom: 1px solid $border-color;

	.nav-item {
		width: 25%;
		border-right: 1px solid $border-color;

		&:nth-child(4n) {
			border-right: none;
		}
	}
}
</style>
