<template>
	<div id="detail">
		<div class="left">
			<ul>
				<li class="first-li" v-for="(firstList,firstIndex) in firstLists">
					<router-link :to="{ path:firstList.path }" >
						<span class="btn" noselect @click="changeFirstShow(firstIndex)" :style="nowFirstIndex===firstIndex?{color:'#000'}:''">
							<i class="first-icon" :style="nowFirstIndex===firstIndex?{backgroundColor:'#000'}:''"></i>
							<span>{{firstList.pagename}}</span>
						</span>
					</router-link>
					<ul v-show="nowFirstIndex===firstIndex">
						
							<li class="secont-li" 
								:style="nowFirstIndex===firstIndex&&nowSconIndex===sconIndex?{backgroundColor:'#699BE4',color:'#fff'}:''"  
								@click="changeScondShow(firstIndex,sconIndex)" v-for="(sconList,sconIndex) in firstList.sconLists"
								>
								<router-link  :to="{ path:sconList.path }" >
									<span  noselect>{{sconList.pagename}}</span>
								</router-link>
							</li>
						
					</ul>
				</li>
			</ul>
		</div>
		<div class="right">
			<router-view/>
		</div>
	</div>
</template>
<script>
import {mapState} from 'vuex'
	export default{
		data(){
			return{
				firstLists:[
					{
						pagename:'首页',
						path:'/index',
						sconLists:[]
					},
					{
						pagename:'广告管理',
						path:'/advertise-campaign',
						sconLists:[
							{
								pagename:'广告策略列表',
								path:'/advertise-campaign'
							},
							{
								pagename:'广告列表',
								path:'/advertise-banner'
							}
						]
					},
					{
						pagename:'数据报表',
						path:'/datacount',
						sconLists:[]
					},
					{
						pagename:'付款',
						path:'/pay',
						sconLists:[]
					},
					{
						pagename:'帐户设置',
						path: '/account',
						sconLists:[]
					}
				]
			}
		},
        computed:mapState({
        	nowFirstIndex(state){
        		return state.detailIndex.nowFirstIndex
        	},
        	nowSconIndex(state){
        		return state.detailIndex.nowSconIndex
        	}
        }),
        watch:{
        	
        },
        methods:{
        	changeFirstShow(firstIndex){ //点击导航栏一级导航触发事件
        		var detailIndex = {//详情页当前的位置
					nowFirstIndex:firstIndex,
					nowSconIndex:0
				}
        		this.$store.commit('setDetailIndex',detailIndex)
        	},
        	changeScondShow(firstIndex,sconIndex){//点击导航栏二级导航触发事件
        		var detailIndex = {//详情页当前的位置
					nowFirstIndex:firstIndex,
					nowSconIndex:sconIndex
				}
        		this.$store.commit('setDetailIndex',detailIndex)
        	}
        },
		created(){
			console.log('details-container.vue is loaded')
		}
	}
</script>
<style lang="scss">
#detail{
	margin-top: 20px;
	position: relative;
	.left{
		border: 1px solid #EEEEEE;
		width: 200px;
		left: 20px;
		top: 0px;
		background-color: #fff;
		position: absolute;
		padding-top: 24px;
		min-height:600px;
		height: 100%;
		font-size: 16px;
		color: #999999;
		ul{
			li{

				span.btn{
					display: inline-block;
					line-height: 64px;
					cursor: pointer;
					width: 100%;
					.first-icon{
						display: inline-block;
						background: #999999;
						border-radius: 4px;
						width: 24px;
						height: 24px;
						margin-right: 10px;
						margin-left: 20px;
					}
				}
				ul{
					li{
						cursor: pointer;
						span{
							display: inline-block;
							line-height:34px;
							font-size: 12px;
							margin-left:53px;
						}
					}
				}
			}
		}
	}
	.right{
		padding-left: 240px;
		padding-right: 20px;
		background-clip:content-box;
	}
}
</style>