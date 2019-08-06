<template>
	<div class="container">
		<!-- v-if="sakura_W_num > 0" -->
		<div class="rule-box" @click="goRule()">活动规则</div>
		<div class="theme-bg"></div>
		<form :report-submit="form_id" @submit="gather" >
			<button class="w-sakura" @click="showSakuraW()" form-type="submit">
				<div class="count-box">
					万能樱
				</div>
				<div class="w-count">{{sakura_W_num}}</div>
			</button>
		</form>
		<div class="reel-box">
			<div v-if="act_status == '1'" class="timer-count">距平分<text style="color: #ea4141">100万</text>还剩{{act_remain_day}}天</div>
			<div v-else class="timer-count">{{act_text}}</div>
			<div class="tips-2">
				大家共集齐<span class="num">{{totalSakuraNum}}朵</span>樱花&nbsp;<span>每朵樱花换1份现金</span>
			</div>
			<div class="flower-box">
				<div class="top">
					<form :report-submit="form_id" @submit="gather" >
						<div class="flower-item" :class="{'disflower': sakura_A_num == '0'}">
							<span>八重樱</span>
							<button v-if="sakura_A_num > 0" class="click-box" form-type="submit"  @click="showSakuraDetail('sakura_a','八重樱','花开时来，花落时也要来。')">
								<div class="num-box">{{sakura_A_num}}</div>
								<div class="dot-box">
									<div class="dot dot-1"></div>
									<div class="dot dot-2"></div>
									<div class="dot dot-3"></div>
									<div class="dot dot-4"></div>
									<div class="dot dot-5"></div>
									<div class="dot dot-6"></div>
									<div class="dot dot-7"></div>
									<div class="dot dot-8"></div>
									<div class="dot dot-9"></div>
								</div>
							</button>

						</div>
					</form>
				</div>
				<div class="center">
					<form :report-submit="form_id" @submit="gather" >
						<div class="flower-item center-left" :class="{'disflower': sakura_E_num == '0'}">
							<span>寒绯樱</span>
							<button  v-if="sakura_E_num > 0" class="click-box" form-type="submit" @click="showSakuraDetail('sakura_e','寒绯樱','不见方三日，世上滿櫻花。')">
								<div class="num-box">{{sakura_E_num}}</div>
								<div class="dot-box">
									<div class="dot dot-1"></div>
									<div class="dot dot-2"></div>
									<div class="dot dot-3"></div>
									<div class="dot dot-4"></div>
									<div class="dot dot-5"></div>
									<div class="dot dot-6"></div>
									<div class="dot dot-7"></div>
									<div class="dot dot-8"></div>
									<div class="dot dot-9"></div>
								</div>
							</button>
						</div>
					</form>
					<form :report-submit="form_id" @submit="gather" >
						<button class="mix-btn" form-type="submit" :class="{'new-mix-btn': is_compose}" @click="showComposeAni()">合成</button>
					</form>
					<form :report-submit="form_id" @submit="gather" >
						<div class="flower-item center-right" :class="{'disflower': sakura_B_num == '0'}">
							<span>吉野樱</span>
							<button  v-if="sakura_B_num > 0" class="click-box" form-type="submit" @click="showSakuraDetail('sakura_b','吉野樱','今日花如雪，山樱如美人。')">
								<div class="num-box">{{sakura_B_num}}</div>
								<div class="dot-box">
									<div class="dot dot-1"></div>
									<div class="dot dot-2"></div>
									<div class="dot dot-3"></div>
									<div class="dot dot-4"></div>
									<div class="dot dot-5"></div>
									<div class="dot dot-6"></div>
									<div class="dot dot-7"></div>
									<div class="dot dot-8"></div>
									<div class="dot dot-9"></div>
								</div>
							</button>
						</div>
					</form>
				</div>
				<div class="bottom">
					<form :report-submit="form_id" @submit="gather" >
						<div class="flower-item bottom-left" :class="{'disflower': sakura_D_num == '0'}">
							<span>淡墨樱</span>
							<button  v-if="sakura_D_num > 0" class="click-box" form-typt="submit" @click="showSakuraDetail('sakura_d','淡墨樱','樱花开处处，想似当年故乡路。')">
								<div class="num-box">{{sakura_D_num}}</div>
								<div class="dot-box">
									<div class="dot dot-1"></div>
									<div class="dot dot-2"></div>
									<div class="dot dot-3"></div>
									<div class="dot dot-4"></div>
									<div class="dot dot-5"></div>
									<div class="dot dot-6"></div>
									<div class="dot dot-7"></div>
									<div class="dot dot-8"></div>
									<div class="dot dot-9"></div>
								</div>
							</button>
						</div>
					</form>
					<form :report-submit="form_id" @submit="gather" >
						<div class="flower-item bottom-right" :class="{'disflower': sakura_C_num == '0'}">
							<span>大岛樱</span>
							<button v-if="sakura_C_num > 0" class="click-box" form-type="submit" @click="showSakuraDetail('sakura_c','大岛樱','梦中繁花犹再现，樱瓣飘飘然。')">
								<div class="num-box">{{sakura_C_num}}</div>
								<div class="dot-box">
									<div class="dot dot-1"></div>
									<div class="dot dot-2"></div>
									<div class="dot dot-3"></div>
									<div class="dot dot-4"></div>
									<div class="dot dot-5"></div>
									<div class="dot dot-6"></div>
									<div class="dot dot-7"></div>
									<div class="dot dot-8"></div>
									<div class="dot dot-9"></div>
								</div>
							</button>
						</div>
					</form>
				</div>
			</div>
			<div class="my-sakura-box" >
				合成的樱花<div class="my-sakura my-sakura-new"><span>X{{sakura_H_num}}</span></div>
			</div>
			<form :report-submit="form_id" @submit="gather" >
				<button class="lottery-btn" form-type="submit" v-if="act_status == '1'" @click="lotterySakura()">
					抽樱花瓣
				</button>
			</form>
			<form :report-submit="form_id" @submit="gather">
				<button class="lottery-btn" form-type="submit" v-if="act_status == '2'" @click="goCash()">
					兑换现金
				</button>
			</form>
			<div class="lottery-btn" v-if="act_status == '0'">
				活动未开始
			</div>
			<div class="lottery-btn" v-if="act_status == '3'">
				活动已结束
			</div>
			<div class="lottery-btn wait-res" v-if="act_status == '4'">
				
			</div>
			<div class="rest-count">
				今日剩余次数<span>{{rest_count || 0}}</span>/{{total_count || 9}}
			</div>
		</div>
		<div class="achieve-box">
			<div class="achieve-top-box">
				<div class="achieve-top-title">集樱花成就解锁</div>
			</div>
			<div v-if="showFaceTime == '1'" class="achieve-content-active" @click="goFaceTime()">
				<img class="achieve-content-active-call" src="https://s5.wandougongzhu.cn/s/e8/1815x_999aff.png" alt="">
			</div>
			<div v-else class="achieve-content">
				<div class="achieve-con-item">
					<div class="flower-box">
						<div v-for="(item, index) in 5" :key="index" class="flower" :class="{'active': index <= progressSakura-1}">

						</div>
					</div>
					<div class="progress">
						<div v-if="progressSakura < 5" class="active" v-bind:style="[{width: progressSakura*40 + 'px',}]"></div>
						<div v-else class="active" style="width: 100%"></div>
					</div>
					<div class="bottom">
						<template v-if="lastSakuraNum > 0">
							<div class="left">大家已集齐<span>{{totalSakuraNum}}</span>朵</div>
							<div class="right">还差<span>{{lastSakuraNum}}</span>朵解锁</div>
						</template>
						<template v-else>
							<div class="center">大家已集齐<span>{{totalSakuraNum}}</span>朵</div>
							<div class="right">解锁成功</div>
						</template>
					</div>
				</div>
			</div>
		</div>
		<div class="task-box">
			<div class="task-title">
				<div>做任务领奖励</div>
				<div class="task-title-tips">完成任务得抽樱花次数</div>
			</div>
			<div class="task-item" v-for="item in taskList" :key="item.task_id">
				<!-- <div v-if="item.task_id == 7" class="task-item-evd task-item-y">不限</div> -->
				<div class="task-item-evd">每日</div>
				<div class="task-item-name">{{item.name}}</div>
				<div class="task-item-img">
					<img v-if="item.task_id == 7" src="https://s4.wandougongzhu.cn/s/03/2x_e99b42.png" alt="">
					<img v-else src="https://s3.wandougongzhu.cn/s/bc/_157403.png" alt="">
				</div>
				<form :report-submit="form_id" @submit="gather" >
					<button v-if="item.status == '0'" form-type="submit" class="task-item-btn receive" @click="getTask(item.task_id)">
						领取
					</button>
				</form>
				<div v-if="item.status == '1'" class="task-item-btn done">
					
				</div>
				<form :report-submit="form_id" @submit="gather" >
					<div v-if="item.status == '-1'" class="task-item-btn">
						<button v-if="item.task_id == '2'" open-type="share" :data-type="1" @click="doTask2()">
							去分享
						</button>
						<button v-if="item.task_id != '2'" form-type="submit" @click="toFinishTask(item.task_id,item.page_id)">
							去完成
						</button>
					</div>
				</form>
				<!-- <div @click="getTask(item.task_id)" v-bind:class="{'task-item-btn': true, 'receive': item.status == '0', 'done': item.status == '1'}">{{item.action_name ? item.action_name : ''}}</div> -->
			</div>
			<div class="task-item task-item-new">
				<div class="suc-box">
					<div class="suc-box-left">
						<div class="task-item-evd task-item-suc">成就</div>
					</div>
					<div class="suc-box-right">
						<div class="task-item-name">邀请好友注册</div>
						<div class="task-item-name">已注册<span>{{inviteCount || 0}}</span>人</div>
					</div>
				</div>
				<div class="task-item-img" @click="showSakuraW()">
					<div v-if="sakura_W_num > 0" class="num">{{sakura_W_num}}</div>
					<img src="https://s.wandougongzhu.cn/s/0e/_16ec47.png" alt="">
				</div>
				<form :report-submit="form_id" @submit="gather" >
					<button class="to-invite" v-bind:class="{'task-item-btn': true}" form-type="submit" @click="showinviteSakuraAll()">去邀请</button>
				</form>
			</div>
		</div>
		<div class="brand-box" v-if="topRankList && topRankList.length > 0">
			<div class="brand-box-title">
				<div>樱花榜</div>
				<div class="brand-title-tips">截止到4月13日，樱花榜TOP5，送日本往返机票</div>
			</div>
			<div class="brand-box-content">
				<div class="brand-box-my">
					<div class="brand-box-top-item">
						<div class="rank">
							<div class="desc">我的排名</div>
							<div class="num">{{userRankList.seq}}</div>
						</div>
						<div class="img-box">
							<img :src="userRankList.imgurl" alt="">
							<div class="name">{{userRankList.nickname}}</div>
						</div>
						<div class="flower-box">
							<div class="flower">{{userRankList.total}}朵</div>
							<div class="time">{{userRankList.last_time}}</div>
						</div>
					</div>
				</div>
				<div class="brand-box-top">
					<div v-for="(item, index) in topRankList" :key="index" class="brand-box-top-item">
						<div class="rank">
							<img v-if="index == 0" src="https://s5.wandougongzhu.cn/s/b2/2x_3236b9.png">
							<img v-if="index == 1" src="https://s3.wandougongzhu.cn/s/27/22x_810409.png">
							<img v-if="index == 2" src="https://s4.wandougongzhu.cn/s/76/32x_35460a.png">
							<div v-if="index > 2" class="last">{{index + 1}}</div>
						</div>
						<div class="img-box">
							<img :src="item.imgurl" alt="">
							<div class="name">{{item.nickname}}</div>
						</div>
						<div class="flower-box">
							<div class="flower">{{item.total}}朵</div>
							<div class="time">{{item.last_time}}</div>
						</div>
					</div>
				</div>
			</div>
		</div>
		<form :report-submit="form_id" @submit="gather" >
			<button class="rec-btn" @click="showGiftRec()" form-type="submit">
				赠领记录
			</button>
		</form>
		<!-- :href="buoy_ad_info.action" -->
		<div class="ad-img-fixed" @click="toFixedCard()">
			<img :src="buoy_ad_info.ad_img" alt="">
		</div>
		<div id="mask" v-if="maskShow">
			<!-- 合成樱花 -->
			<div class="compose-box" v-if="showAlert == 'compose'">
				<div class="compose-tips">
					恭喜获得一朵樱花
				</div>
				<div class="compose-ani"></div>
				<div class="compose-ani-2"></div>
				<div class="compose-ani-3"></div>
				<div class="shink"></div>
				<div class="shink2"></div>
				<form :report-submit="form_id" @submit="gather" >
					<button class="compose-btn" form-type="submit" @click="closeAlert()">确定</button>
				</form>
			</div>
			<!-- 点击**樱花瓣弹框 -->
			<div class="to-alert-box" v-if="showAlert == 'sakuraDetail'">
				<div class="colse" @click="closeAlert()"></div>
				<div class="sakura-text">
					<div class="name">{{sakuraDetailName}}</div>
					<div class="poetry">{{sakuraDetailPoetry}}</div>
				</div>
				<!-- <div class="mysakura" v-bind:style="{transform: 'rotate('+sakuraDetailRotate+'deg)'}"></div> -->
				<img class="mysakura" v-bind:class="{'rotate1': sakuraDetailKey == 'sakura_b','rotate2': sakuraDetailKey == 'sakura_c','rotate3': sakuraDetailKey == 'sakura_d','rotate4': sakuraDetailKey == 'sakura_e'}" src="https://s5.wandougongzhu.cn/s/e0/myflower1_485615.png">
				<div class="mysakura-tips">
					<p>每天首次赠送可获得一次抽樱花瓣的机会</p>
					<p>取消分享也会扣除樱花瓣，一定完成分享哦~</p>
				</div>
				<form :report-submit="form_id" @submit="gather" >
					<button class="mysakura-btn" form-type="submit" @click="sendToFriendShow()">
						送给好友
					</button>
				</form>
			</div>
			<!-- 恭喜你获得了**樱 -->
			<div class="get-alert-box" v-if="showAlert == 'lotteryRes'">
				<div class="colse" @click="closeAlert()"></div>
				<div class="mysakura-text">
					<div class="congratulation">恭喜你，获得了</div>
					<div class="name">{{lottery_res.sakura_name}}</div>
				</div>
				<div class="getsakura">

				</div>
				<!-- <img class="getsakura" src="https://s5.wandougongzhu.cn/s/e0/myflower1_485615.png"> -->
				<form :report-submit="form_id" @submit="gather" >
					<button class="mysakura-btn" form-type="submit" @click="closeAlert()">
						确定
					</button>
				</form>
			</div>
			 <!-- 恭喜获得万能樱 -->
			<div class="get-alert-box" v-if="showAlert == 'sakuraAll'">
				<div class="colse" @click="closeAlert()"></div>
				<div class="mysakura-text">
					<div class="congratulation">恭喜你，获得了</div>
					<div class="name">万能樱</div>
				</div>
				<div class="universal">
					<div class="dot-box">
						<div class="dot dot-1"></div>
						<div class="dot dot-2"></div>
						<div class="dot dot-3"></div>
						<div class="dot dot-4"></div>
						<div class="dot dot-5"></div>
						<div class="dot dot-6"></div>
						<div class="dot dot-7"></div>
						<div class="dot dot-8"></div>
						<div class="dot dot-9"></div>
					</div>
					<!-- <img class="getsakura" src="https://s5.wandougongzhu.cn/s/e0/myflower1_485615.png"> -->
				</div>
				<form :report-submit="form_id" @submit="gather" >
					<button form-type="submit" class="mysakura-btn">
						确定
					</button>
				</form>
			</div>
			 <!-- 邀请好友得万能樱 -->
			 <!-- inviteSakuraAllShow -->
			<div class="get-alert-box" v-if="showAlert == 'inviteSakuraAll'">
				<div class="colse" @click="closeAlert()"></div>
				<div class="invite-text">
					<div class="invite-title">邀请好友注册得万能樱</div>
					<div>万能樱可兑换任意一朵花瓣</div>
				</div>
				<img class="getsakura invite-sakura" src="https://s2.wandougongzhu.cn/s/9f/wan_ebbf7a.png">
				<form :report-submit="form_id" @submit="gather" >
					<button class="invite-btn" form-type="submit" open-type="share" :data-type="2">
						去邀请
					</button>
				</form>
				<div class="universal-tips">花瓣在好友验证手机号后发放</div>
			</div>
			<!-- 万能樱兑换 -->
			<div class="get-alert-box" v-if="showAlert == 'sakuraAllChange'">
				<div class="colse" @click="closeAlert()"></div>
				<div class="mysakura-text">
					<div class="universal-compose">请选择樱花瓣</div>
					<div class="universal-tips">使用1个万能樱可以兑换任意1朵花瓣</div>
				</div>
				<div class="flower-box universal-flower">
					<div class="top">
						<div class="flower-item" :class="{'choosed': sakura_whitch_choosed == 'sakura_a'}" @click="chooseChangeSakura('sakura_a')">
							<span v-if="sakura_A_num > 0" class="have-flower-num">{{sakura_A_num}}</span>
							<span>八重樱</span>
						</div>
					</div>
					<div class="center">
						<div class="flower-item center-left" :class="{'choosed': sakura_whitch_choosed == 'sakura_e'}" @click="chooseChangeSakura('sakura_e')">
							<span v-if="sakura_E_num > 0" class="have-flower-num">{{sakura_E_num}}</span>
							<span>寒绯樱</span>
						</div>
						<div class="flower-item center-right" :class="{'choosed': sakura_whitch_choosed == 'sakura_b'}" @click="chooseChangeSakura('sakura_b')">
							<span v-if="sakura_B_num > 0" class="have-flower-num">{{sakura_B_num}}</span>
							<span>吉野樱</span>
						</div>
					</div>
					<div class="bottom">
						<div class="flower-item bottom-left" :class="{'choosed': sakura_whitch_choosed == 'sakura_d'}" @click="chooseChangeSakura('sakura_d')">
							<span v-if="sakura_D_num > 0" class="have-flower-num">{{sakura_D_num}}</span>
							<span>淡墨樱</span>
						</div>
						<div class="flower-item bottom-right" :class="{'choosed': sakura_whitch_choosed == 'sakura_c'}" @click="chooseChangeSakura('sakura_c')">
							<span v-if="sakura_C_num > 0" class="have-flower-num">{{sakura_C_num}}</span>
							<span>大岛樱</span>
						</div>
					</div>
				</div>
				<form :report-submit="form_id" @submit="gather" >
					<button class="mysakura-btn" form-type="submit" @click="changeSakura()">
						兑换
					</button>
				</form>
			</div>
			<!-- 赠领记录 -->
			<!-- giftRecShow -->
			<div class="get-alert-box" v-if="showAlert == 'giftRec'">
				<div class="colse" @click="closeAlert()"></div>
				<div class="gift-res-title">
					赠领记录
				</div>
				<div class="gift-res-content">
					<div v-if="giftRecList && giftRecList.length > 0">
						<div class="gift-res-item" v-for="(item,index) in giftRecList" :key="index">
							<div v-if="item.type == '1'">
								<div v-if="item.from_user_nickname" class="rec">赠送的<span>{{item.sakura_name}}</span>被<span>{{item.from_user_nickname}}</span>领取了</div> 
								<div v-if="!item.from_user_nickname" class="rec">赠送的<span>{{item.sakura_name}}</span>待领取<button class="reshare" open-type="share" :data-type="0" :data-sakuraid="item.sakura_id" :data-sakurakey="item.sakura_key" :data-sakuraname="item.sakura_name">继续赠送</button> </div> 
							</div> 
							<div v-if="item.type == '2'">
								<div class="rec">领取了<span>{{item.from_user_nickname}}</span>的<span>{{item.sakura_name}}</span></div> 
							</div> 
							<div class="time">{{item.mtime}}</div>
						</div>
					</div>
					<div class="gift-res-item-null" v-if="giftRecList.length == 0">
						暂时没有赠领记录哦，快去分享给好友吧～
					</div>
				</div>
				<form :report-submit="form_id" @submit="gather" >
					<button class="mysakura-btn" form-type="submit" @click="closeAlert()">
						确定
					</button>
				</form>
			</div>
			<!-- 好友送你一朵**樱 -->
			<!-- inviteShareSakura -->
			<div class="get-alert-box" v-if="showAlert == 'inviteShareSakura'">
				<div class="colse" @click="closeAlert()"></div>
				<div class="mysakura-text">
					<div class="congratulation">好友<span>{{inviteUser}}</span>送你一朵</div>
					<div class="name">{{inviteShareSakuraName}}</div>
				</div>
				<div class="getsakura">

				</div>
				<!-- <img class="getsakura" src="https://s5.wandougongzhu.cn/s/e0/myflower1_485615.png"> -->
				<form :report-submit="form_id" @submit="gather" >
					<button class="mysakura-btn" form-type="submit" @click="checkAuth()">
						领取
					</button>
				</form>
			</div>
			<!-- 来晚了樱花已经被领取了 -->
			<!-- showHaveDone -->
			<div class="get-alert-box suc-alert-box" v-if="showAlert == 'showHaveDone'">
				<div class="colse" @click="closeAlert()"></div>
				<div class="mysakura-text">
					<div class="name">手慢了，花瓣已被别人领取了</div>
				</div>
				<form :report-submit="form_id" @submit="gather" >
					<button class="mysakura-btn" form-type="submit" @click="closeAlert()">
						确定
					</button>
				</form>
			</div>
			<!-- 分享成功告诉好友 -->
			<div class="get-alert-box suc-alert-box" v-if="showAlert == 'sendToFriend'">
				<div class="colse" @click="closeAlert()"></div>
				<div class="mysakura-text mysakura-text-done">
					<div class="name">樱花瓣已扣除，快去分享给好友吧！</div>
				</div>
				<form :report-submit="form_id" @submit="gather" >
					<button open-type="share" :data-type="0" class="mysakura-btn">
						确定
					</button>
				</form>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			form_id:true,
			user_id: '',
			userInfo: {},
			flowerStatus: '0',
			status: '-1',
			text: '',
			sakura_A_num: 0, //八重樱
			sakura_B_num: 0, //吉野樱
			sakura_C_num: 0, //大岛樱 
			sakura_D_num: 0, //淡墨樱
			sakura_E_num: 0, //寒绯樱
			sakura_W_num: 0, //万能樱数量
			sakura_G_num: 0, //赠送花瓣数量
			sakura_H_num: 0, //合成樱花数量
			is_compose: false, //是否可以合成樱花
			rest_count: 0, //剩余抽奖次数
			total_count: 9, //今日可抽总次数
			lottery_res: {}, //抽取樱花瓣结果
			maskShow: false, //蒙层
			taskList: [],
			totalSakuraNum: 0,
			lastSakuraNum: 500000,
			progressSakura: 0, //集樱花进度0-5代表0w-50w
			restDay: 10,
			restText: '',
			lock: false,
			sakuraDetailKey: 'sakura_a',
			sakuraDetailRotate: 0, //旋转角度
			sakuraDetailName: '八重樱',
			sakuraDetailPoetry: '花开时来，花落时也要来。',
			shareImg: 'https://s.wandougongzhu.cn/s/54/-02_a336b2.jpg', //分享图
			shareImgBtn: {
				'sakura_a': 'https://s2.wandougongzhu.cn/s/7d/__1_de53f5.jpg',
				'sakura_b': 'https://s.wandougongzhu.cn/s/c8/__2_209e10.jpg',
				'sakura_c': 'https://s5.wandougongzhu.cn/s/58/__3_b21b66.jpg',
				'sakura_d': 'https://s.wandougongzhu.cn/s/10/__4_6eaacb.jpg',
				'sakura_e': 'https://s5.wandougongzhu.cn/s/41/__5_4165fc.jpg'
			},//分享花瓣给好友图了list
			shareSakura: 'sakura_a',
			sakura_All_num: 0, //万能花瓣数量
			sakura_whitch_choosed: '',
			exchange_sakura_key: '', //要兑换的花瓣
			inviteCount: 0, //邀请好友数量
			ruleShowMore: false,
			ruleShowText: '展开更多',
			giftRecList: [], //赠领记录
			invite_sakura: '', //通过邀请来领取的花瓣key
			invite_user_id: '', //邀请人id
			option: '',
			inviteUser: '', //好友昵称
			inviteShareSakuraName: '', //好友送的**盈
			sakura_id: '',
			checkInfo: '',
			haveDone: false,
			recv_id: '',
			showAlert: '',
			act_status: '0', // 0未开始 1进行中 2 兑换 3结束
			act_text: '', //活动文案
			act_remain_day: 0, //活动剩余X天！
			index_ad_info: '', //首页广告
			buoy_ad_info: '', //悬浮广告or底部广告
			cloundShareActInfo: {}, //云控分享页面
			cloundShareSakuraInfo: {}, //云控分享花瓣
			topRankList: [], //排行榜数据
			userRankList: {}, //当前用户的排行数据
			showFaceTime: '0', //是否显示山下久智FaceTime
			pageId: 19767, //活动规则卡片页id
			interval:'',
			position: {},
		};
	},
	onLoad() {
		let ch = 'sakura_mp_2019';
		wx.hideShareMenu();
		wx.setStorage({ key: 'ch', data: ch });
		WMP.globalData.ch = ch;
		//浏览打点
		Net.tick({
			type: 'sakura_uv',
			page_name: 'sy',
		},'sakura');
		// this.getRestDay();
		this.option = this.$root.$mp.query;
		console.log(this.$root.$mp);
		if (!WMP.globalData.userInfo || !WMP.globalData.userInfo.user_id) {
			let is_first = wx.getStorageSync('is_first_access');
			if(is_first == '0'){
				console.log(is_first);
			}else{
				Net.tick({
					type:'sakura_access'
				},'sakura');
				wx.setStorage({
					key:"is_first_access",
					data:"0"
				});
			}
			this.showGetSakuraAlert();
			if (this.option.sakura_key) {
				this.maskShow = true;
				this.showAlert = 'inviteShareSakura';
			}
		} else {
			if (this.option.user_id == WMP.globalData.userInfo.user_id) {
				if (this.option.sakura_id) {
					wx.showToast({
						title: '不能领取自己分享的花瓣～',
						icon: 'none',
						duration: 2000
					});
					this.closeAlert();
				} else {
					this.getUserActInfo();
				}
			} else {
				this.getUserActInfo();
				if (this.option.sakura_key) {
					this.maskShow = true;
					this.showAlert = 'inviteShareSakura';
				}
			}
		}
	},
	onShow() {
		this._getUserActInfo();
	},
	onShareAppMessage (res) {
		let self = this;
		this.closeAlert();
		if (res.from == 'button' && res.target.dataset.type == '0') {
			if (res.target.dataset.sakuraid) {
				Net.tick({
					type:'sakura_share_flower',
				},'sakura');
				console.log('data-sakuraid='+ res.target.dataset.sakuraid);
				return {
					title: '送你一朵'+res.target.dataset.sakuraname + this.cloundShareSakuraInfo.title,
					path: '/pages/fireworks/fireworks?sakura_key=' + res.target.dataset.sakurakey +'&user_id=' + this.user_id +"&sakura_id=" + res.target.dataset.sakuraid + '&ch=sakura_mp_2019',
					imageUrl: this.shareImgBtn[res.target.dataset.sakurakey],
					success: function () {
						self.shareActivity();
					},
					fail: function () {
						wx.showToast({
							title: '取消分享',
							icon: 'error',
							duration: 2000
						});
					}
				};
			} else {
				console.log('this-sakura_id='+this.sakura_id);
				Net.tick({
					type:'sakura_share_flower',
				},'sakura');
				return {
					title: '送你一朵'+this.sakuraDetailName + this.cloundShareSakuraInfo.title,
					path: '/pages/fireworks/fireworks?sakura_key=' + this.sakuraDetailKey +'&user_id=' + this.user_id +"&sakura_id=" + this.sakura_id + '&ch=sakura_mp_2019',
					imageUrl: this.shareImgBtn[this.sakuraDetailKey],
					success: function () {
						
						self.shareActivity();
					},
					fail: function () {
						wx.showToast({
							title: '取消分享',
							icon: 'error',
							duration: 2000
						});
					}
				};
			}
			
		} else {
			let shareImg = this.shareImg;

			if (res.from == 'menu') {
				return {
					title: this.cloundShareActInfo.title + this.act_text + '!',
					path: '/pages/fireworks/fireworks?user_id=' + this.user_id + '&ch=sakura_mp_2019',
					imageUrl: shareImg,
					success: function (res) {
						Net.tick({
							type:'sakura_share_act',
						},'sakura');
						self.shareActivity();
						self.getUserActInfo();
					},
					fail: function () {
						wx.showToast({
							title: '取消分享',
							icon: 'error',
							duration: 2000
						});
					}
				}
			} else {
				if (res.target.dataset.type && res.target.dataset.type == '1') {
					Net.tick({
						type:'sakura_task',
						sakura_task_id: 2
					},'sakura');
					return {
						title: this.cloundShareActInfo.title + this.act_text + '!',
						path: '/pages/fireworks/fireworks?user_id=' + this.user_id + '&ch=sakura_mp_2019',
						imageUrl: shareImg,
						success: function (res) {
						
							//任务二
							self.shareActivity();
							self.getUserActInfo();
						},
						fail: function () {
							wx.showToast({
								title: '取消分享',
								icon: 'error',
								duration: 2000
							});
						}
					};
				} else if (res.target.dataset.type && res.target.dataset.type == '2') {
					Net.tick({
						type: 'sakura_share_act',
					},'sakura');
					return {
						title: this.cloundShareActInfo.title + this.act_text + '!',
						path: '/pages/fireworks/fireworks?user_id=' + this.user_id + '&ch=sakura_mp_2019',
						imageUrl: shareImg,
						success: function (res) {
							self.shareActivity();
							self.getUserActInfo();
						},
						fail: function () {
							wx.showToast({
								title: '取消分享',
								icon: 'error',
								duration: 2000
							});
						}
					};
				}
			
			}
			
		}
	},
	onPullDownRefresh: function () {
		wx.stopPullDownRefresh();
		if (WMP.globalData.userInfo && WMP.globalData.userInfo.user_id) {
			this.getUserActInfo();
		}
	},
	methods: {
		goCash() {
			WMP.checkAuthPromise(this.$root.$mp.page).then(() => {
				wx.navigateTo({ 
					url: '/pages/tocash/tocash' 
				});
			})
		},
		doTask2() {
			Net.tick({
				type:'sakura_task',
				sakura_task_id: 2
			},'sakura');
			this.shareActivity();
			this.getUserActInfo();
		},
		goFaceTime() {
			console.log('facetime 666')
			WMP.checkAuthPromise(this.$root.$mp.page).then(()=>{
				let url = `https://m.wandougongzhu.cn/activity/sweets?from_act=sakura`
				let real_url = `/page/webview/index?url=${encodeURIComponent(url)}`;
				Net.tick({
					type:'sakura_go_facetime',
				},'sakura');
				wx.navigateTo({ url: real_url });
			})
		},
		goRule(){
			wx.navigateTo({ url: `/page/page/index?page_id=${this.pageId}` });
		},
		shareActivity() {
			console.log('share act')
			Net.get('Sakura.userShareActivity', {
				data: {
					user_id: this.user_id
				}
			}).then(res=>{
				if(res.errno=='0') {
					wx.showToast({
						title: '分享成功',
						icon: 'success',
						duration: 3000
					});
				} else {
					wx.showToast({
						title: res.errmsg,
						icon: 'error',
						duration: 2000
					});
				}
			});
		},
		toFixedCard() {
			Net.tick({
				type:'sakura_go_ad',
			},'sakura');
			if (this.buoy_ad_info.page_id && this.buoy_ad_info.page_id != '0') {
				wx.navigateTo({ url: `/page/page/index?page_id=${this.buoy_ad_info.page_id}` });
			} else {
				wx.switchTab({ url: '/page/index/index'});
			}
		},
		gather(e) {
			console.log(e.mp.detail.formId);
			Net.gatherMsgId({
				scene_id: 7,
				scene_val: 'sakura',
				form_id: e.mp.detail.formId,
			});
		},
		sendToFriendShow() {
			this.showAlert = 'sendToFriend';
			this.getShareSakuraId();
		},
		getShareSakuraId() {
			Net.get('Sakura.userGiftSakura', {
				data: {
					user_id: this.user_id,
					sakura_key: this.sakuraDetailKey
				}
			}).then(res=>{
				if(res.errno=='0') {
					this.sakura_id = res.data.sakura_id;
				} else {
					wx.showToast({
						title: res.errmsg,
						icon: 'error',
						duration: 2000
					});
				}
			});
		},
		showGetSakuraAlert() {
			console.log('sakura act info')
			Net.get('Sakura.getUserActivityInfoByUserId', {
				data: {
					user_id: '0',
					from_user_id:  this.option.user_id || '0',
					sakura_id: this.option.sakura_id || '0'
				}
			}).then(res=>{
				if(res.errno=='0') {
					this.taskList = res.data.day_task;
					let infoList = res.data.info;
					this.topRankList = res.data.top_list;
					this.userRankList = res.data.user_seq || {};
					this.sakura_A_num = infoList.sakura_a;
					this.sakura_B_num = infoList.sakura_b;
					this.sakura_C_num = infoList.sakura_c;
					this.sakura_D_num = infoList.sakura_d;
					this.sakura_E_num = infoList.sakura_e;
					this.sakura_W_num = infoList.sakura_w;
					this.sakura_H_num = parseInt(infoList.sakura_h);
					this.sakura_G_num = infoList.sakura_g;
					if (infoList.sakura_a > 0 && infoList.sakura_b > 0 && infoList.sakura_c > 0 && infoList.sakura_d > 0 && infoList.sakura_e >0 ) {
						this.is_compose = true;
					} else {
						this.is_compose = false;
					}				
					this.rest_count = infoList.residue_lottery_count;
					this.total_count = infoList.day_total;
					// this.user_id = infoList.user_id;
					this.totalSakuraNum = res.data.h_sakura_count;
					this.inviteCount = res.data.info.invite_count;
					this.inviteUser = res.data.gift_sakura.gift_user_name;
					this.inviteShareSakuraName = res.data.gift_sakura.sakura_name;
					this.recv_id = res.data.gift_sakura.recv_user_id;
					this.act_status = res.data.activity_status;
					this.act_text = res.data.activity_status_text;
					this.act_remain_day = res.data.activity_remain_day;
					this.index_ad_info = res.data.index_ad_info;
					this.buoy_ad_info = res.data.buoy_ad_info;
					this.cloundShareActInfo = res.data.share_activity;
					this.cloundShareSakuraInfo = res.data.share_sakura;
					this.lastSakuraNum = parseInt(500000 - parseInt(res.data.h_sakura_count));
					this.progressSakura = parseFloat(parseInt(res.data.h_sakura_count)/100000);
					this.showFaceTime = res.data.show_facetime;
				} else {
					wx.showToast({
						title: res.errmsg,
						icon: 'error',
						duration: 2000
					});
				}
			});
		},
		checkAuth() {
			if (WMP.globalData.userInfo && WMP.globalData.userInfo.user_id) {
				if (this.option.user_id == this.user_id ) {
					if (this.option.sakura_id) {
						Net.tick({
							type:'sakura_get_flower',
							is_succ : 0  // fail
						},'sakura');
						wx.showToast({
							title: '不能领取自己分享的花瓣～',
							icon: 'none',
							duration: 2000
						});
						this.closeAlert();
					} else {
						this.getUserActInfo();
					}
				} else {
					if (this.recv_id == "" || this.recv_id == '0') {
						Net.get('Sakura.userRecvGiftSakura', {
							data: {
								user_id: this.user_id,
								from_user_id: this.option.user_id,
								sakura_id: this.option.sakura_id
							}
						}).then(res=>{
							if(res.errno=='0') {
								Net.tick({
									type:'sakura_get_flower',
									is_succ : 0  // suc
								},'sakura');
								wx.showToast({
									title: '领取成功',
									icon: 'success',
									duration: 2000
								});
								this.closeAlert();
								this.getUserActInfo();
							} else {
								wx.showToast({
									title: res.errmsg,
									icon: 'error',
									duration: 2000
								});
							}
						});
					} else {
						this.showAlert = 'showHaveDone';
						this.maskShow = true;
						Net.tick({
							type:'sakura_get_flower',
							is_succ : 1  // fail
						},'sakura');
					}
				}
			} else {
				this.closeAlert();
				this.showAlert = '';

				// getInfo().then(()=> {
					this.$root.$mp.page.data['inviterId'] = this.option.user_id;
					this.$root.$mp.page.data['curGoods'] = {goods_id: 0};
					WMP.checkAuthPromise(this.$root.$mp.page).then((res)=>{
						this.userInfo = WMP.globalData.userInfo;
						this.user_id = this.userInfo.user_id;
						this.bindInviteUser();
						this.closeAlert();
						this.checkAuth();
					});
				// });
			}
		},
		getUserActInfo() {
			this.maskShow = false;

			// WMP.checkAuthPromise(this.$root.$mp.page).then((res)=> {
				Net.tick({
					type:'sakura_access1'
				},'sakura');
				if (WMP.globalData.userInfo && WMP.globalData.userInfo.user_id) {
					this._getUserActInfo();
				} else {
					WMP.checkAuthPromise(this.$root.$mp.page).then(()=>{
						this.bindInviteUser();
						// this._getUserActInfo();
					}).catch((error) => {
						console.error(error);
					})
				}
			// })
		},
		_getUserActInfo() {
			if (WMP.globalData.userInfo && WMP.globalData.userInfo.user_id) {
				this.userInfo = WMP.globalData.userInfo;
				this.user_id = this.userInfo.user_id;
				Net.get('Sakura.getUserActivityInfoByUserId', {
					data: {
						user_id: this.user_id,
						from_user_id:  this.option.user_id || '0',
						sakura_id: this.option.sakura_id || '0'
					}
				}).then(res=>{
					if(res.errno=='0') {
						this.taskList = res.data.day_task;
						let infoList = res.data.info;
						this.topRankList = res.data.top_list;
						this.userRankList = res.data.user_seq;
						this.sakura_A_num = infoList.sakura_a;
						this.sakura_B_num = infoList.sakura_b;
						this.sakura_C_num = infoList.sakura_c;
						this.sakura_D_num = infoList.sakura_d;
						this.sakura_E_num = infoList.sakura_e;
						this.sakura_W_num = infoList.sakura_w;
						this.sakura_H_num = parseInt(infoList.sakura_h);
						this.sakura_G_num = infoList.sakura_g;
						if (infoList.sakura_a > 0 && infoList.sakura_b > 0 && infoList.sakura_c > 0 && infoList.sakura_d > 0 && infoList.sakura_e >0 ) {
							this.is_compose = true;
						} else {
							this.is_compose = false;
						}				
						this.rest_count = infoList.residue_lottery_count;
						this.total_count = infoList.day_total;
						// this.user_id = infoList.user_id;
						this.totalSakuraNum = res.data.h_sakura_count;
						this.inviteCount = res.data.info.invite_count;
						this.inviteUser = res.data.gift_sakura.gift_user_name;
						this.inviteShareSakuraName = res.data.gift_sakura.sakura_name;
						this.recv_id = res.data.gift_sakura.recv_user_id;
						this.act_status = res.data.activity_status;
						this.act_text = res.data.activity_status_text;
						this.act_remain_day = res.data.activity_remain_day;
						this.index_ad_info = res.data.index_ad_info;
						this.buoy_ad_info = res.data.buoy_ad_info;
						this.cloundShareActInfo = res.data.share_activity;
						this.cloundShareSakuraInfo = res.data.share_sakura;
						this.lastSakuraNum = parseInt(500000 - parseInt(res.data.h_sakura_count));
						this.progressSakura = parseFloat(parseInt(res.data.h_sakura_count)/100000);
						this.showFaceTime = res.data.show_facetime;
					} else if (res.errno == '2008') {
						WMP.checkAuthPromise(this.$root.$mp.page);
					} else {
						wx.showToast({
							title: res.errmsg,
							icon: 'error',
							duration: 2000
						});
					}
				});
			} else {
				this.bindInviteUser();
			}
		},
		bindInviteUser() {
			if(WMP.globalData.userInfo && WMP.globalData.userInfo.user_id) {
				Net.post('Share.setInviterFromMp', {
          data:{
            goods_id: '0',
            inviter_id: this.option.user_id,
            invite_coupon_id: 820
          }
				}).then((res)=>{
					if(res.errno == 0) {
						this._getUserActInfo();
						console.log('bind success');
					}
				});
			}
		},
		getRestDay() {
			let myDate = new Date();
			let m = myDate.getMonth();
			let d = myDate.getDate();
			if (d < 11) {
				this.restDay = 11 - d;
				this.restText = '距离分钱还剩'+this.restDay+'天';
			} else if (d > 10 && d < 14) {
				this.restDay = 0;
				this.restText = '正在撒钱中';
			} else {
				this.restDay = -1;
				this.restText = '活动已结束';
			}
		},
		showHaveDone() {
			this.maskShow = true;
			this.showAlert = 'showHaveDone';
			Net.tick({
				type:'sakura_get_flower',
				is_succ : 1  // fail
			},'sakura');
		},
		showSakuraDetail(key, name, poetry) {
			if (this.act_status == '1') {
				this.sakuraDetailKey = key;
				this.sakuraDetailName = name;
				this.sakuraDetailPoetry = poetry;
				if(this.sakuraDetailKey == 'sakura_a') {
					this.sakuraDetailRotate = 0;
				} else if (this.sakuraDetailKey == 'sakura_b') {
					this.sakuraDetailRotate = 72;
				} else if (this.sakuraDetailKey == 'sakura_c') {
					this.sakuraDetailRotate = 144;
				} else if (this.sakuraDetailKey == 'sakura_d') {
					this.sakuraDetailRotate = -144;
				} else if (this.sakuraDetailKey == 'sakura_e') {
					this.sakuraDetailRotate = -72;
				}
				this.maskShow = true;
				this.showAlert = 'sakuraDetail';
			} else {
				wx.showToast({
					title: '抽樱花已结束',
					icon: 'error',
					duration: 2000
				});
			}
			
		},
		showComposeAni() {
			if (this.is_compose) {
				Net.get('Sakura.userComposeSakura', {
					data: {
						user_id: this.user_id
					}
				}).then(res=>{
					if(res.errno=='0') {
						this.maskShow = true;
						this.showAlert = 'compose';
					} else {
						wx.showToast({
							title: res.errmsg,
							icon: 'none',
							duration: 2000
						});
					}
				}) 
			} else {
				wx.showToast({
					title: '樱花数量不足～',
					icon: 'none',
					duration: 2000
				});
			}
		},
		//万能瓣兑换弹框
		showSakuraW() {
			this.maskShow = true;
			this.showAlert = 'sakuraAllChange';
		},
		//获得万能瓣弹框
		showSakuraAll() {
			this.maskShow = true;
			this.showAlert = 'sakuraAll';
		},
		//邀请好友得万能樱弹框
		showinviteSakuraAll() {
			this.maskShow = true;
			this.showAlert = 'inviteSakuraAll';
		},
		showMoreRule() {
			this.ruleShowMore = !this.ruleShowMore;
		},
		showGiftRec() {
			// getInfo().then((res)=> {
				// console.info(res);
				// this.$root.$mp.page.data['userInfo'] = {user_id: '1'};
				this.$root.$mp.page.data['inviterId'] = this.option.user_id;
				this.$root.$mp.page.data['curGoods'] = {goods_id: 0};
				if (WMP.globalData.userInfo && WMP.globalData.userInfo.user_id) {
					this._showGiftRec();
				} else {
					WMP.checkAuthPromise(this.$root.$mp.page).then(()=>{
						this.bindInviteUser();
						this._showGiftRec();
					}).catch((error) => {
						console.error(error);
					})
				}
			// })
			
		},
		_showGiftRec() {
			this.userInfo = WMP.globalData.userInfo;
			this.user_id = this.userInfo.user_id;
			
			Net.get('Sakura.getUserGiftSakuraList', {
				data: {
					user_id: this.user_id
				}
			}).then(res=>{
				if(res.errno=='0') {
					this.giftRecList = res.data;
					this.maskShow = true;
					this.showAlert = 'giftRec';
				} else {
					wx.showToast({
						title: res.errmsg,
						icon: 'error',
						duration: 2000
					});
				}
			});
		},
		chooseChangeSakura(param) {
			this.sakura_whitch_choosed = param;
			this.exchange_sakura_key = param;
		},
		closeAlert (param) {
			param = false;
			this.maskShow = false;
			this.getUserActInfo();
		},
		shareSakura() {

		},
		_lotterySakura() {
			//todo
			if (this.rest_count == '0') {
				wx.showToast({
					title: '赶紧去做任务，领取抽奖机会吧～',
					icon: 'none',
					duration: 3000
				});
			} else {
				this.userInfo = WMP.globalData.userInfo;
				this.user_id = this.userInfo.user_id;
				Net.post('Sakura.userLotterySakura', {
					user_id: this.user_id
				}).then(res=>{
					if(res.errno=='0') {
						this.maskShow = true;
						this.showAlert = 'lotteryRes';
						this.lottery_res = res.data;
					} else {
						wx.showToast({
							title: res.errmsg,
							icon: 'none',
							duration: 3000
						});
					}
				});
			}
		},
		lotterySakura() {
			var self = this;
			if (WMP.globalData.userInfo && WMP.globalData.userInfo.user_id) {
				self._lotterySakura();
			} else {
				// getInfo().then((res)=> {
					
					// this.$root.$mp.page.data['userInfo'] = {user_id: '1'};
					this.$root.$mp.page.data['inviterId'] = this.option.user_id;
					this.$root.$mp.page.data['curGoods'] = {goods_id: 0};

					WMP.checkAuthPromise(this.$root.$mp.page).then((res)=>{
						console.log('lotterySakura');
						self.bindInviteUser();
						// self._getUserActInfo();
						self._lotterySakura();
					});
				// })
			}
		},
		changeSakura() {
			
			if (this.exchange_sakura_key) {
				if (this.sakura_W_num > 0) {
					Net.get('Sakura.userExchangeSakuraW', {
						data: {
							user_id: this.user_id,
							exchange_sakura_key: this.exchange_sakura_key
						}
					}).then(res=>{
						if(res.errno=='0') {
							this.maskShow = false;
							this.showAlert = '';
							this.getUserActInfo();
							wx.showToast({
								title: '兑换成功',
								icon: 'success',
								duration: 1500,
							});
						} else {
							wx.showToast({
								title: res.errmsg,
								icon: 'error',
								duration: 2000
							});
						}
					});
				} else {
					wx.showToast({
						title: '万能樱不足～',
						icon: 'error',
						duration: 1500,
					})
				}
			} else {
				wx.showToast({
					title: '请选择一个花瓣',
					icon: 'error',
					duration: 1500,
				});
			}
		},
		getTask(task_id) {
			var paramTask = task_id;
			Net.post('Sakura.userRecvTask',{
				data: {
					user_id: this.user_id,
					task_id: paramTask
				}
			}).then(res=>{
				if(res.errno=='0') {
					Net.tick({
						type:'sakura_task',
						sakura_task_id: parseInt(paramTask)
					},'sakura');
					wx.showToast({
						title: '领取成功',
						icon: 'success',
						duration: 1500,
					});
					this.getUserActInfo();
				} else {
					wx.showToast({
						title: res.errmsg,
						icon: 'error',
						duration: 2000
					});
				}
			});
		},
		toFinishTask(task_id,page_id) {
			WMP.checkAuthPromise(this.$root.$mp.page).then(()=>{
				Net.tick({
					type:'sakura_task',
					sakura_task_id: parseInt(task_id)
				},'sakura');
				if (task_id == 3) {
					if (this.sakura_A_num == '0' && this.sakura_B_num == '0' && this.sakura_C_num == '0' && this.sakura_D_num == '0' && this.sakura_E_num == '0') {
						wx.showToast({
							title: '当前没有花瓣～',
							icon: 'none',
							duration: 1500,
						});
					} else {
						wx.navigateTo({
							url: '/pages/togift/togift',
						});
					}
				} else{
					if (page_id && page_id != '0') {
						wx.navigateTo({ url: `/page/page/index?page_id=${page_id}`});
					} else {
						wx.switchTab({ url: '/page/index/index'});
					}
					
				}
			})
		},
	},

};
</script>


<style scoped>
button::after{ border: none; }
@font-face {
    font-family: "SakuraFont";
    src: url("https://s5.wandougongzhu.cn/s/72/fonts_80bdfb.eot"); /* IE9 */
    src: url("https://s5.wandougongzhu.cn/s/72/fonts_80bdfb.eot?#iefix") format("embedded-opentype"), /* IE6-IE8 */
	url("https://s5.wandougongzhu.cn/s/2e/fonts_ec2f0d.ttf") format("truetype"), /* chrome, firefox, opera, Safari, Android, iOS 4.2+ */
    url("https://s5.wandougongzhu.cn/s/34/fonts_953a8a.woff") format("woff"); /* chrome, firefox */
    font-style: normal;
    font-weight: normal;
}
@font-face {
    font-family: "SakuraKai";
    src: url("https://s5.wandougongzhu.cn/s/6f/kai_1c4989.eot"); /* IE9 */
    src: url("https://s5.wandougongzhu.cn/s/6f/kai_1c4989.eot?#iefix") format("embedded-opentype"), /* IE6-IE8 */
	url("https://s5.wandougongzhu.cn/s/53/kai_190fb4.ttf") format("truetype"), /* chrome, firefox, opera, Safari, Android, iOS 4.2+ */
    url("https://s5.wandougongzhu.cn/s/da/kai_68ad47.woff") format("woff"); /* chrome, firefox */
    font-style: normal;
    font-weight: normal;
}
@font-face {
    font-family: "SakuraPang";
    src: url("https://s5.wandougongzhu.cn/s/30/pang_3fda36.eot"); /* IE9 */
    src: url("https://s5.wandougongzhu.cn/s/30/pang_3fda36.eot?#iefix") format("embedded-opentype"), /* IE6-IE8 */
	url("https://s5.wandougongzhu.cn/s/f1/pang_ece31c.ttf") format("truetype"), /* chrome, firefox, opera, Safari, Android, iOS 4.2+ */
    url("https://s5.wandougongzhu.cn/s/54/pang_c7e928.woff") format("woff"); /* chrome, firefox */
    font-style: normal;
    font-weight: normal;
}
/* body {
	font-family: "SakuraKai";
} */
.rule-top-box {
	width: 100%;
	background: url('https://s4.wandougongzhu.cn/s/99/26_836fb3.png') no-repeat;
	background-position: top;
	background-size: 100%;
}
.ad-img-fixed {
	/* position: fixed; */
	/* right: 10px;
	bottom: 10px; */
	width: 345px;
	height: 130px;
	margin: 35px auto 110px auto;
}

.ad-img-fixed img {
	width: 100%;
	height: 100%;
}
.ad-img-box {
	display: block;
	width: 100%;
	border: none;
}
.ad-img-box img {
	width: 100%;
	max-width: 100%;
	max-height: 100%;
	height: 150px;
}
.invite-text {
	font-family: "sakuraKai";
	font-size: 12px;
	color: rgb(67, 67, 67);
	margin: 30px auto 20px auto;
}
.invite-text .invite-title {
	font-size: 15px;
}
.rule-p-title {
	font-size: 16px;
	font-weight: bold;
	margin: 15px auto 5px auto;
}
.rule-show-more { 
	width: 60px;
	height: 20px;
	margin: 0 auto;
	text-align: center;
	padding-right: 10px;
	background: url('https://s3.wandougongzhu.cn/s/94/arrow_44a7ec.png') no-repeat;
	background-position: right center;
	background-size: 10px;
}
.shouqi {
	background: url('https://s3.wandougongzhu.cn/s/f8/arraw_2b1964.png') no-repeat;
	background-position: right center;
	background-size: 10px;
}
.faq-title {
	 font-size: 16px;
	 font-weight: bold;
	 margin: 5px;
}
.faq-q {
	color: rgb(243, 81, 109);
	margin-top: 5px;
}
.my-sakura-box {
	/* width: 100px; */
	font-size: 14px;
	color: rgb(88, 94, 141);
	font-weight: bold;
	font-family: "sakuraKai";
	text-align: center;
	margin: -30px auto 0 auto;
	display: flex;
	justify-content: center;
}
.my-sakura {
	width: 15px;
	height: 15px;
	margin: 2px 3px;
}
.my-sakura-new {
	background: url('https://s3.wandougongzhu.cn/s/7e/4_88421d.png') no-repeat;
	background-size: cover;
}
.my-sakura-new span {
	padding-left: 20px;
}
.w-sakura {
	position: absolute;
	right: 10px;
	top: 127px;
	width: 30px;
	height: 80px;
	background: url('https://s5.wandougongzhu.cn/s/f9/_5b6c81.png') no-repeat;
	background-size: 100% 100%;
	animation: flutter 3s linear 2.8s infinite alternate;
	margin: 0;
	padding: 0;
	text-align: center;
	z-index: 1;
	box-sizing: border-box;
}
.w-sakura .count-box {
	position: relative;
	width: 20px;
	height: 45px;
	margin: 15px 5px 0 5px;
	font-size: 15px;
	font-family: "sakuraKai";
	text-align: center;
	line-height: 15px;
	color: rgb(76, 38, 24);
}
.w-sakura .w-count {
	/* width: 20px; */
	margin: 3px 10px 0 10px;
	line-height: 12px;
	color: rgb(255, 29, 95);
	text-align: center;
	display: flex;
	justify-content: center;
	/* position: absolute;
	bottom: 7px; */
}
.timer-count {
	width: 100%;
	height: 30px;
	line-height: 30px;
	font-size: 18.5px;
	color: rgb(66, 75, 143);
	text-align: center;
	/* margin: 30px auto 4px auto; */
	font-family: 'SakuraPang';
	padding-top: 30px;
}
.colse {
	position: absolute;
	top: -45px;
	right: 0px;
	width: 30px;
	height: 50px;
	background: url('https://s2.wandougongzhu.cn/s/5f/_977ab3.png') no-repeat;
	z-index: 2;
	background-size: contain;
	cursor: pointer;
}
.num-box, .task-item-img .num, .have-flower-num {
	width: 20px;
	height: 20px;
	text-align: center;
	line-height: 20px;
	color: #fff;
	background: url('https://s1.wandougongzhu.cn/s/00/5_b08501.png') no-repeat;
	background-size: cover;
	font-size:14px;
	position:absolute;
	right:0;
}
.to-alert-box,.get-alert-box,.compose-box {
	position: absolute;
	left: 50%;
	top: 50%;
	transform: translate(-50%,-50%);
	width: 280px;
	height: 345px;
	font-size: 14px;
	font-weight: normal;
	text-align: center;
	background: url('https://s3.wandougongzhu.cn/s/65/alertbg_701e5c.png') no-repeat;
	background-size: cover;
	z-index: 3;
}
.get-alert-box {
	background: url('https://s2.wandougongzhu.cn/s/f9/alertbg2_587294.png') no-repeat;
	background-size: cover;
}
.suc-alert-box {
	height: 190px;
	background: url('https://s.wandougongzhu.cn/s/e8/alert_230438.png') no-repeat;
	background-size: 100% 100%;
}
.suc-alert-box  .mysakura-text .name {
	font-size: 12px;
	margin-top: 20px;
}
.compose-box {
	position: absolute;
	width: 375px;
	height: 400px;
	background: none;
}

.compose-tips {
	font-size: 28px;
	font-family: "sakuraKai";
	color: #fff;
	margin: 0 auto;
	top: 0;
	-webkit-animation: showtext 5s ease-in-out;
	animation: showtext 5s ease-in-out;
	/* animation-delay: 4s; */
}
.compose-btn {
	z-index: 10;
	position: absolute;
	left: 50%;
	bottom: 0;
	font-family: "sakuraKai";
	transform: translate(-50%, 0);
	width: 115px;
	height: 38px;
	line-height: 38px;
	font-size: 14px;
	color: #fff;
	margin: 0 auto;
	background: url('https://s2.wandougongzhu.cn/s/68/toyou_3d05c2.png') no-repeat;
	background-size: cover;
	-webkit-animation: showtext 5s ease-in-out;
	animation: showtext 5s ease-in-out;
	/* animation-delay: 4s; */
}
.universal {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%,-50%);
	width: 375px;
	height: 400px;
	z-index: 1;
	background: url('https://s5.wandougongzhu.cn/s/c8/_8612fe.png') no-repeat;
	background-size: 375px 400px;
	background-position: center;
}
.universal .dot-box {
	width: 80px;
	height: 50px;
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%,-50%) scale(1.5);
}

.universal-compose {
	font-size: 23px;
}
.sakura-text {
	display: flex;
}
.universal-tips {
	font-size: 12px;
	line-height: 20px;
}
.congratulation {
	font-size: 14px;
	line-height: 25px;
}
.gift-res-title {
	font-size: 24px;
	font-weight: bold;
	margin-top: 25px;
}
.gift-res-content {
	height: 220px;
	overflow-y: scroll;
	font-size: 12px;
	text-align: left;
	margin: 10px 20px;
}
.gift-res-item {
	position: relative;
	overflow: hidden;
	height: 50px;
	border-bottom: 1px solid rgba(233, 233, 233,.5);
}
.gift-res-item .rec {
	height: 30px;
	display: inline-block;
	line-height: 30px;
	font-size: 14px;
	white-space: nowrap;
}
.gift-res-item .rec span {
	color: rgb(234, 60, 98);
}
.gift-res-item .rec .reshare {
	position: absolute;
	right: 0;
	top: 0;
	display: block;
	width: 50px;
	height: 20px;
	margin: 15px auto;
	padding: 0;
	border-radius: 0;
	font-size: 12px;
	color: #fff;
	text-align: center;
	line-height: 20px;
	background: url('https://s2.wandougongzhu.cn/s/68/toyou_3d05c2.png') no-repeat;
	background-size: 100% 100%;
}
.gift-res-item .time {
	line-height: 20px;
	color: rgb(153, 153, 153);
}
.gift-res-item-null {
	font-size: 12px;
	margin: 50px auto;
}
.mysakura-text {
	margin-top: 25px;
}
.mysakura-text .name{
	font-family: "SakuraFont";
	font-size: 22px;
	line-height: 22px;
}
.mysakura-text-done {
	margin: 80px auto;
}
.sakura-text .poetry {
	position: absolute;
	left: 16px;
	top: 15px;
	width: 14px;
	font-family: "SakuraKai";
	color: #191919;
	font-size: 12px;
	line-height: 16px;
	writing-mode: vertical-lr;
}

.sakura-text .name {
	position: absolute;
	left: 36px;
	top: 15px;
	width: 25px;
	height: 75px;
	font-family: "SakuraFont";
	font-size: 25px;
	line-height: 25px;
	font-weight: normal;
}
.mysakura,.getsakura{
	width: 120px;
	height: 160px;
	position: relative;
	margin: 50px auto 30px auto;
	background: url('https://s5.wandougongzhu.cn/s/e0/myflower1_485615.png') no-repeat;
	background-size: cover;
}
.getsakura {
	margin: 30px auto;
}
.mysakura-tips {
	width: 100%;
	position: absolute;
	color: rgb(111, 111, 111);
	bottom: 70px;
	font-size: 12px;
	font-family: "SakuraKai";
	text-align: center;
	font-weight: normal;
}
.mysakura-btn {
	position: absolute;
	left: 50%;
	transform: translate(-50%,0);
	bottom: 15px;
	width: 115px;
	height: 38px;
	line-height: 38px;
	font-size: 16px;
	color: #fff;
	background: url('https://s2.wandougongzhu.cn/s/68/toyou_3d05c2.png') no-repeat;
	background-size: 100% 100%;
	margin: 0 auto;
}
.invite-sakura {
	width: 100px;
	height: 150px;
	margin: 0px auto;
	background: none;
}
.invite-btn {
	width: 115px;
	height: 38px;
	line-height: 38px;
	color: #fff;
	position: relative;
	border: none;
	border-radius: 0;
	background: url('https://s2.wandougongzhu.cn/s/68/toyou_3d05c2.png') no-repeat;
	background-size: 100% 100%;
	margin: 10px auto;
}
.rule-box {
	position: absolute;
	left: 0;
	top: 10px;
	width: 75px;
	height: 24px;
	text-align: center;
	line-height: 25px;
	background: url('https://s2.wandougongzhu.cn/s/72/258_97adc7.png') no-repeat;
	background-size: 100% 100%;
	font-size: 10px;
	font-family: "SakuraKai";
	color: #FFFFFF;
	z-index: 999;
}
/* .celendar {
	width: 350px;
	height: 240px;
	margin: 0 auto;
	z-index: 1;
}
.red-umbrella {
	position: absolute;
	left: 0;
	top: 0;
	width: 32px;
	height: 110px;
	z-index: 0;
}
.rule-content {
	font-family: "SakuraKai";
	font-size: 13px;
	color: #191919;
	line-height: 1.6;
	text-align: left;
	margin: 0 15px;
}
.rule-content .rule-p-title {
	margin-top: 15px;
}
.rule-content p {
	margin: 5px 0;
} */
.achieve-top-box,.brand-box-title {
	width: 345px;
	height: 50px;
	margin: 10px auto;
	font-size: 21px;
	font-family: "SakuraKai";
	background: url(https://s1.wandougongzhu.cn/s/e6/26_687fb2.png) no-repeat;
	background-size: 100% 35px;
	background-position: center;
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	position: relative;
}
.achieve-content {
	position: relative;
	width: 355px;
	height: 185px;
	margin: 0 auto;
	background: url(https://s5.wandougongzhu.cn/s/78/15x_988a30.png) no-repeat;
	background-size: 100% 100%;
}
.achieve-content-active {
	position: relative;
	width: 355px;
	height: 125px;
	margin: 0 auto;
	background: url(https://s4.wandougongzhu.cn/s/60/215x_a4a1b6.png) no-repeat;
	background-size: 100% 100%;
}
.achieve-content-active-call {
	position: absolute;
	width: 140px;
	height: 48px;
	right: 50px;
	bottom: 15px;
	animation: breath 1s ease 1s infinite;
}
.achieve-con-item {
	width: 200px;
	margin: 0 15px;
	position: absolute;
	bottom: 15px;
	display: flex;
	flex-direction: column;
	justify-content: flex-start;
	align-items: flex-end;
}
.achieve-con-item .flower-box {
	width: inherit;
	margin: 0 auto;
	display: flex;
	justify-content: space-between;
}
.achieve-con-item .flower-box .flower {
	width: 25px;
	height: 25px;
	background: url(https://s1.wandougongzhu.cn/s/c1/2x_3f7479.png) no-repeat;
	background-size: 100%;
	margin: 5px;
}
.achieve-con-item .flower-box .flower.active {
  color: rgb(237, 61, 98);
	background: url(https://s3.wandougongzhu.cn/s/3e/2x_6141d6.png) no-repeat;
	background-size: cover;
}
.achieve-con-item .progress {
	position: relative;
	width: inherit;
	height: 5px;
	border-radius: 2px;
  background-color: rgb(255, 232, 234);
	margin: 5px auto;
}
.achieve-con-item .progress .active {
	position: absolute;
	left: 0;
	top: 0;
	width: 0%;
	height: 5px;
	border-radius: 2px;
	background-color: rgb(245, 107, 132);
}
.achieve-con-item .bottom {
	width: inherit;
	margin: 0 auto;
	color: #9e9e9e;
	font-size: 10px;
	display: flex;
	justify-content: space-between;
}
.achieve-con-item .bottom .active {
  color: rgb(232, 70, 107);
}
.rec-btn {
	display: block;
	font-size: 18px;
	font-family: "SakuraKai";
	width: 117px;
	height: 35px;
	line-height: 35px;
	margin: 15px auto 35px auto;
	color: #fff;
	border: 1px solid rgba(66, 80, 128,.5);
	background-color: rgb(95, 109, 156);
	background: url('https://s3.wandougongzhu.cn/s/01/_2fd8c9.png') no-repeat;
	background-size: cover;
}
#mask {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	background: rgba(0,0,0,.8);
}
.container {
	/* position: relative; */
	font-weight: bold;
	width: 100%;
	height: 100%;
	text-align: center;
	padding: 0;
	margin: 0;
	background: url('https://s3.wandougongzhu.cn/s/af/2x_22d7e5.png') no-repeat;
	background-size: 100% auto;
	background-color: #f3f2f1;
	padding-top: 115px;
}
.tips {
	margin-top: 90px;
	font-size: 16px;
	color: rgb(237, 61, 98);
	text-align: center;
	font-weight: bold;
}
.tips-2 {
	margin: 5px auto 0 auto;
	font-size: 10px;
	color: rgb(88, 94, 141);
	font-weight: bold;
}
.tips-2 .num {
	color: rgb(237, 61, 98);
}
.reel-box {
	width: 358px;
	height: 480px;
	background: url(https://s5.wandougongzhu.cn/s/75/_2f85f2.png) no-repeat;
	background-size: 100% 100%;
	position: relative;
}
.reel-box .flower-box {
	margin-top: 15px;
	font-family: "sakuraFont";
}
.reel-box .flower-box .flower-item {
	width: 75px;
	height: 100px;
	text-align: center;
}
.flower-box .top {
	text-align: center;
}
.flower-box .top .flower-item {
	margin: 4px auto;
	position: relative;
}
.flower-item {
	width: 75px;
	height: 100px;
	background: url(https://s5.wandougongzhu.cn/s/6a/flower_d713db.png) no-repeat;
	background-size: cover;
	background-position: center;
} 
.flower-item .click-box{
	display: block;
	width:inherit;
	height:inherit;
	background: none;
}
.flower-item span {
	font-size: 14px;
	color: #fff;
	position:absolute;
	bottom: 25px;
	left: 50%;
	transform: translate(-50%,0);
	width: 50px;
}
.flower-item.disflower {
	background: url('https://s.wandougongzhu.cn/s/ab/disFlower_c08dae.png') no-repeat;
	background-size: cover;
	background-position: center;
}
.flower-item.disflower span {
	color: rgba(255, 255, 255, 0.2);
}
.flower-item.bottom-left span,.flower-item.bottom-right span{
	transform: rotate(180deg);
	margin-left: -25px;
}

.flower-item span.have-flower-num {
	position: absolute;
	top: 0;
	left: auto;
	right: 0;
	width: 15px;
	height: 15px;
	font-size: 12px;
	line-height: 15px;
	background: url('https://s1.wandougongzhu.cn/s/00/5_b08501.png') no-repeat;
	background-size: cover;
}
.universal-flower {
	margin-top: 20px;
	font-family: "sakuraFont";
}

.universal-flower .flower-item {
	width: 60px;
	height: 80px;
	color: rgba(255, 255, 255, 0.4);
	/* background: url(' https://s5.wandougongzhu.cn/s/e6/disflower-no_67817f.png') no-repeat; */
	background: url('https://s3.wandougongzhu.cn/s/30/disflower_94699c.png') no-repeat;
	background-size: cover;
	background-position: center;
}
.universal-flower .flower-item.choosed {
	background: url('https://s5.wandougongzhu.cn/s/e0/myflower1_485615.png') no-repeat;
	background-size: cover;
	background-position: center;
}
.universal-flower .flower-item span {
	color: rgba(255, 255, 255, 0.4);
}
.universal-flower .flower-item.choosed span {
	color: rgba(255, 255, 255, 1);
}
.universal-flower .flower-item span.have-flower-num {
	color: rgba(255, 255, 255, 1);
}
.dot{
	position:relative;
	width: 4px;
	height: 4px;
	background: #FFFFFF;
    border-radius: 50%;
	background: radial-gradient(rgba(255,255,255,1),rgba(255,255,255,0));
	animation: twinkling 1.5s infinite ease-in-out;
	-webkit-animation: twinkling 1.5s infinite ease-in-out;
 } 
 .dot-1 {
	 transform: scale(0.8);
	 top: 40px;
	 left: 25px;
	 animation-delay: 0.8s;
 } 
 .dot-2 {
	 transform: scale(1.2);
	 top: 25px;
	 left: 45px;
	 animation-delay: 1s;
 } 
 .dot-3 {
	 top: 35px;
	 left: 50px;
 } 
 .dot-4 {
	 transform: scale(1.3);
	 top: 30px;
	 left: 35px;
	 animation-delay: 0.5s;
 } 
 .dot-5 {
	 top: 35px;
	 left: 60px;
	 animation-delay: 1s;
 } 
 .dot-6 {
	 top: 35px;
	 left: 20px;
 } 
 .dot-7 {
	 top: 35px;
	 left: 35px;
	 animation-delay: 0.3s;
 } 
 .dot-8 {
	 transform: scale(1.6);
	 top: 40px;
	 left: 50px;
	 animation-delay: 1.3s;
 } 
 .dot-9 {
	 transform: scale(1.5);
	 top: 40px;
	 left: 25px;
 } 
 @keyframes twinkling{  
    0%{  
        opacity: 0;  
    }
	20% {
		opacity: 0.4;
	}
	50% {
		opacity: 1;
	}
	80% {
		opacity: 0.4;
	}
    100%{  
        opacity: 0;  
    }  
} 
 @-webkit-keyframes twinkling{  
    0%{  
        opacity: 0;  
    }
	20% {
		opacity: 0.4;
	}
	50% {
		opacity: 1;
	}
	80% {
		opacity: 0.4;
	}
    100%{  
        opacity: 0;  
    }  
}
@keyframes breath {
  from {
    transform: scale(1);
  }
  50% {
    transform: scale(1.1);
  }
  to {
    transform: scale(1);
  }
}
.center {
	display: flex;
	justify-content: center;
}
.center-left {
	position: relative;
	top: -40px;
	left: -12px;
	transform: rotate(-72deg);
}
.center-left .num-box,.center-left span.have-flower-num {
	transform: rotate(72deg);
}
.center-right {
	position: relative;
	top: -40px;
	left: 12px;
	transform: rotate(72deg);
}
.center-right .num-box,.center-right span.have-flower-num  {
	left: 0;
	right: auto;
	transform: rotate(-72deg);
}
.mix-btn {
	display: block;
	width: 75px;
	height: 75px;
	color: rgba(255, 255, 255, 0.302);
	font-size: 20px;
	line-height: 75px;
	background: url('https://s1.wandougongzhu.cn/s/d1/_ca6d40.png') no-repeat;
	background-size: cover;
	font-family: "sakuraKai";
}
.new-mix-btn {
	color: rgba(255,255,255,1);
	background: url('https://s4.wandougongzhu.cn/s/a0/2_77ea79.png') no-repeat;
	background-size: cover;
}
.flower-box .bottom {
	display: flex;
	justify-content: center;
}
.bottom-left {
	position: relative;
	top: -38px;
	left: -15px;
	transform: rotate(-144deg);
}
.bottom-left .num-box,.bottom-left span.have-flower-num{
	transform: rotate(144deg);
}
.bottom-right {
	position: relative;
	top: -38px;
	left: 15px;
	transform: rotate(144deg);
}
.bottom-right .num-box,.bottom-right span.have-flower-num {
	left: 0;
	right: auto;
	transform: rotate(-144deg);
}
.bottom-right span.have-flower-num {
	left: 25px;
}
.universal-flower .center-left {
	left:-40rpx;
}
.universal-flower .center-right {
	left:40rpx;
}
.universal-flower .bottom-left {
	top: -60px;
	left: 2px;
}
.universal-flower .bottom-right {
	top: -60px;
	left: 4px;
}
.rest-count {
	/* width: 100px; */
	color: rgb(88, 94, 141);
	font-size: 12px;
	font-family: "SakuraKai";
	text-align: center;
	margin: 10px auto;
	position: relative;
}
.lottery-btn {
	font-size: 18px;
	font-family: "SakuraKai";
	display: block;
	width: 140px;
	height: 35px;
	line-height: 35px;
	color: #fff;
	text-align: center;
	background: url('https://s2.wandougongzhu.cn/s/68/toyou_3d05c2.png') no-repeat;
	background-size: 100% 100%;
	margin: 5px auto;
}
.lottery-btn.wait-res {
	background: url('https://s5.wandougongzhu.cn/s/98/_46346a.png') no-repeat;
	background-size: 100% 100%;
}
.task-title,.rule-title {
	position: relative;
	width: 345px;
	height: 50px;
	line-height: 40px;
	margin: 10px auto;
	font-size: 21px;
	font-family: "SakuraKai";
	color: #191919;
	font-weight: bold;
	background: url('https://s1.wandougongzhu.cn/s/e6/26_687fb2.png') no-repeat;
	background-size: 100% 35px;
	background-position: center;
	display: flex;
	flex-direction: column;
	align-content: center;
}
.rule-title {
	background: none;
}
.task-title-tips,.brand-title-tips {
	position: relative;
	text-align: center;
	color: rgb(118, 109, 109);
	font-size: 10px;
	top: -20px;
}
.brand-title-tips {
	top: 0;
}
.task-item {
	width: 345px;
	height: 60px;
	font-size: 15px;
	font-family: "SakuraKai";
	line-height: 60px;
	color: #191919;
	margin: 10px auto;
	display: flex;
	background: url('https://s5.wandougongzhu.cn/s/88/_849809.png') no-repeat;
	background-size: 100% 100%;
}
.task-item-new {
	background: url('https://s2.wandougongzhu.cn/s/dd/_c6edb3.png') no-repeat;
	background-size: 100% 100%;
}
.task-item-evd,.task-item-suc {
	width: 37px;
	height: 20px;
	font-size: 12px;
	line-height: 20px;
	margin: 20px 10px;
	background: url('https://s.wandougongzhu.cn/s/82/evd_641d28.png') no-repeat;
	background-size: cover;
	text-align: center;
	color: #fff;
}
.task-item-y {
	/* margin:  0px 10px; */
	background: url('https://s.wandougongzhu.cn/s/00/932x_9e4c97.png') no-repeat;
	background-size: cover;
}
.task-item-suc {
  color: #ff8a00;
	margin:  0px 10px;
	background: url('https://s4.wandougongzhu.cn/s/ed/942x_91051c.png') no-repeat;
	background-size: cover;
}
.task-item-suc .task-item-name {
	line-height: 20px;
}
.task-item-name {
	font-size: 14px;
}
.suc-box-right .task-item-name {
	line-height: 20px;
}
.suc-box {
	line-height: 30px;
	display: flex;
	/* flex-direction: column; */
}
.suc-box-left {
	display: flex;
	margin-top: 20px;
}
.suc-box-right {
	font-size: 14px;
	text-align: left;
	margin: 10px 0;
}

.task-item-img {
	position: absolute;
	right: 110px;
	margin: 3px 0;
}
.task-item-img img {
	width: 50px;
	height: 54px;
}
.task-item-btn {
	position: absolute;
	right: 10px;
	width: 65px;
	height: 30px;
	margin: 15px;
	font-size: 14px;
	line-height: 30px;
	/* color: rgb(73, 15, 0); */
	color: #fff;
	text-align: center;
	background: url('https://s1.wandougongzhu.cn/s/f2/done_be011c.png') no-repeat;
	background-size: 100%;
	padding: 0;
	display: block;
}
.task-item-btn.done {
	background: url('https://s2.wandougongzhu.cn/s/82/8_cff9fd.png')
		no-repeat;
	background-size: contain;
	background-position: center;
}
.task-item-btn.receive {
	color: rgb(73, 15, 0);
	background: url('https://s5.wandougongzhu.cn/s/f8/ing_fe1225.png') no-repeat;
	background-size: 100% 100%;
}
.task-item-btn button {
	display: block;
	font-size: 14px;
	line-height: 30px;
	padding: 0;
	/* font-style: "SakuraKai"; */
	/* color: rgb(73, 15, 0); */
	color: #fff;
	background-color:rgba(255,255,255,0);
	border: none;
}
.to-invite {
	color: rgb(73, 15, 0);
	background: url('https://s5.wandougongzhu.cn/s/f8/ing_fe1225.png') no-repeat;
	background-size: 100% 100%;
}
.rotate1 {
	transform: rotate(72deg);
}
.rotate2 {
	transform: rotate(144deg);
}
.rotate3 {
	transform: rotate(-144deg);
}
.rotate4 {
	transform: rotate(-72deg);
}
#mask {
	/* visibility: hidden; */
	text-align: center;
	display: flex;
	justify-content: center;
	align-items: center;
	z-index: 2;
}
.compose-ani, .compose-ani-2, .compose-ani-3,.shink,.shink2 {
	opacity: 0;
	position: absolute;
	width: 300px;
	height: 300px;
	margin: 10px 37px;
	background: url('https://s3.wandougongzhu.cn/s/ac/3_d1bd5d.png') no-repeat;
	background-size: cover;
	-webkit-animation: compose 3s ease-in-out;
	animation: compose 3s ease-in-out;
}
.compose-ani-2 {
	opacity: 0;
	z-index: 2;
	background: url('https://s2.wandougongzhu.cn/s/c8/cool6_6d080f.png') no-repeat;
	background-size: cover;
	-webkit-animation: compose-2 4s;
	animation: compose-2 4s;
	transform: scale(2);
	/* animation-delay: 2s; */
}
.compose-ani-3 {
	opacity: 1;
	z-index: 3;
	background: url('https://s1.wandougongzhu.cn/s/73/hua_11b087.png') no-repeat;
	background-size: cover;
	-webkit-animation: compose-3 4s;
	animation: compose-3 4s;
	/* animation-delay: 3s; */
}
.shink {
	z-index: 2;
	background: url('https://s5.wandougongzhu.cn/s/93/shink2_7a1dbd.png') no-repeat;
	background-size: cover;
	transform: scale(2);
	-webkit-animation: shink 0.5s infinite ease-in-out;
	animation: shink 0.5s infinite ease-in-out;
	animation-delay: 4s;
}
.shink2 {
	z-index: 2;
	background: url('https://s3.wandougongzhu.cn/s/bb/shink3_9c3028.png') no-repeat;
	background-size: cover;
	transform: scale(2);
	-webkit-animation: shink2 0.5s infinite ease-in-out;
	animation: shink2 0.5s infinite ease-in-out;
	animation-delay: 4s;
}
@keyframes shink{
    0%{  
        opacity: 1;
    }
    100%{  
        opacity: 0;
    }  
} 
@-webkit-keyframes shink{
    0%{  
        opacity: 1;
    }
    100%{  
        opacity: 0;
    }  
} 
@keyframes showtext {
	0%{  
        opacity: 0;
	}
	80% {
		opacity: 0;
	}
    100%{  
        opacity: 1;
    } 
}
@-webkit-keyframes showtext{
    0%{  
        opacity: 0;
	}
	80% {
		opacity: 0;
	}
    100%{  
        opacity: 1;
    }  
} 

@keyframes shink2{
    0%{  
        opacity: 0;
    }
    100%{  
        opacity: 1;
    }  
} 
@-webkit-keyframes shink2{
    0%{  
        opacity: 0;
    }
    100%{  
        opacity: 1;
    }  
} 
@keyframes compose{
    0%{  
        opacity: 1;
		transform: scale(1) rotate(0);
    }
	/* 66.6% {
		opacity: 1;
		transform: scale(1) rotate(720deg);
	} */
    100%{  
        opacity: 0;  
		transform: scale(0.2) rotate(1080deg);
    }  
} 
 @-webkit-keyframes compose{  
    0%{  
        opacity: 1;
		transform: scale(0.2) rotate(0);
    }
	/* 66.6% {
		opacity: 1;
		transform: scale(1) rotate(720deg);
	} */
    100%{  
        opacity: 0.2;  
		transform: scale(0.2) rotate(720deg);
    }  
} 
@keyframes compose-2{
    0%{  
        opacity: 0;
		transform: scale(0.4) rotate(0);
    }
	50%{
		opacity: 0.2;
		transform: scale(0.4) rotate(720deg);
	}
    100%{  
        opacity: 1;  
		transform: scale(2) rotate(1440deg);
    }  
}
@-webkit-keyframes compose-2{
    0%{  
        opacity: 0;
		transform: scale(0.4) rotate(0);
    }
	50%{
		opacity: 0.2;
		transform: scale(0.4) rotate(720deg);
	}
    100%{  
        opacity: 1;  
		transform: scale(2) rotate(1440deg);
    } 
}
@keyframes compose-3{
    0%{  
        opacity: 0;
		transform: scale(0.2);
    }
	75%{
		opacity: 0;
		transform: scale(0.2);
	}
    100%{  
        opacity: 1;  
		transform: scale(1);
    }  
}
@-webkit-keyframes compose-3{
   	0%{  
        opacity: 0;
		transform: scale(0.2);
    }
	75%{
		opacity: 0;
		transform: scale(0.2);
	}
    100%{  
        opacity: 1;  
		transform: scale(1);
    } 
}
@-webkit-keyframes flutter
{
    0% {
        transform: rotate(2deg);
        -webkit-transform: rotate(2deg);
        transform-origin: 50% 0;
        -webkit-transform-origin: 50% 0;
    }
    20% {
        transform: rotate(10deg);
        -webkit-transform: rotate(10deg);
        transform-origin: 50% 0;
        -webkit-transform-origin: 50% 0;
    }
    40% {
        transform: rotate(0deg);
        -webkit-transform: rotate(0deg);
        transform-origin: 50% 0;
        -webkit-transform-origin: 50% 0;
    }
    60% {
        transform: rotate(-2deg);
        -webkit-transform: rotate(-2deg);
        transform-origin: 50% 0;
        -webkit-transform-origin: 50% 0;
    }
    80% {
        transform: rotate(-10deg);
        -webkit-transform: rotate(-10deg);
        transform-origin: 50% 0;
        -webkit-transform-origin: 50% 0;
    }
    100% {
        transform: rotate(0deg);
        -webkit-transform: rotate(0deg);
        transform-origin: 50% 0;
        -webkit-transform-origin: 50% 0;
    }
}
@keyframes flutter
{
    0% {
        transform: rotate(2deg);
        -webkit-transform: rotate(2deg);
        transform-origin: 50% 0;
        -webkit-transform-origin: 50% 0;
    }
    20% {
        transform: rotate(10deg);
        -webkit-transform: rotate(10deg);
        transform-origin: 50% 0;
        -webkit-transform-origin: 50% 0;
    }
    40% {
        transform: rotate(0deg);
        -webkit-transform: rotate(0deg);
        transform-origin: 50% 0;
        -webkit-transform-origin: 50% 0;
    }
    60% {
        transform: rotate(-2deg);
        -webkit-transform: rotate(-2deg);
        transform-origin: 50% 0;
        -webkit-transform-origin: 50% 0;
    }
    80% {
        transform: rotate(-10deg);
        -webkit-transform: rotate(-10deg);
        transform-origin: 50% 0;
        -webkit-transform-origin: 50% 0;
    }
    100% {
        transform: rotate(0deg);
        -webkit-transform: rotate(0deg);
        transform-origin: 50% 0;
        -webkit-transform-origin: 50% 0;
    }
}
.brand-box {
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
}
.brand-box-content {
	width: 360px;
	height: 385px;
	padding: 20px 0;
	background: url(https://s.wandougongzhu.cn/s/17/_aebe2c.png) no-repeat;
	background-size: 100% 100%;
	margin: 0 auto;
	color: rgb(25, 25, 25);
  font-size: 16px;
}
.brand-box-top{
	width: 345px;
	margin: 0 auto;
	display: flex;
	flex-direction: column;
	justify-content: center;
	flex-wrap: wrap;
}
.brand-box-top-item,.brand-box-my{
	position: relative;
	width: 310px;
	height: 63px;
	margin: 0 auto;
	display: flex;
	align-items: center;
	justify-content: space-between;
	border-bottom: 0.5px solid rgb(220, 220, 220);
}
.brand-box-top-item:first-child,.brand-box-top-item:last-child {
	border-bottom: none;
}
.brand-box-my {
	width: 6.9rem;
	margin: 0 auto;
	height: 75px;
  box-shadow: 0px 5px 6px 0px rgba(52, 52, 52, 0.1);
}
.brand-box-my .brand-box-top-item {
	border-bottom: 0px;
}
.brand-box-top-item .img-box {
	width: 150px;
	font-size: 12px;
	display: flex;
	flex-direction: row;
	justify-content: center;
	align-content: center;
}
.brand-box-top-item .img-box img{
	position: relative;
	width: 40px;
	height: 40px;
	margin: 0 5px;
	border-radius: 50%;
	border: 2px solid rgb(108, 108, 108);
	box-sizing: border-box;
}

.brand-box-top-item .img-box .name {
	width: 100px;
	max-width: 100px;
	overflow: hidden;
	text-overflow: ellipsis;
	display: flex;
	align-items: center;
}
.brand-box-top-item .rank {
	width: 56px;
	height: 56px;
	margin: auto 10px;
	font-size: 10px;
	color: #000000;
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
}
.brand-box-top-item .rank img {
	width: 50px;
	height: 50px;
	margin: 3px;
}
.brand-box-top-item .rank .num {
	color: #ea4141;
	font-size: 15px;
}
.brand-box-top-item .rank .last {
	width: 20px;
	height: 20px;
	border-radius: 50%;
	text-align: center;
	font-size: 15px;
	color: #ffffff;
	background: rgb(235, 58, 120);
}
.brand-box-top-item .flower-box {
	flex: 1;
	text-align: right;
	display: flex;
	flex-direction: column;
	justify-content: flex-end;
	align-items: center;
}
.brand-box-top-item .flower-box .flower {
	color: #ea4141;
	font-size: 12px;
	width: 100%;
}
.brand-box-top-item .rank .desc,.brand-box-top-item .flower-box .time {
  color: rgb(158, 158, 158);
  font-size: 8px;
	white-space: nowrap;
}
.theme-bg {
	position: absolute;
	top: 0;
	width: 100%;
	height: 145px;
	background: transparent;
	background-size: 100% 100%;
	z-index: 1;
	font-size: 30px;
	color: #fff;
}
</style>

 