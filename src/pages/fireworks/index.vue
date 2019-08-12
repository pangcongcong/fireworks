import card from '@/components/card';
<template>
	<div class="container">
		<div class="rule-box" @click="goRule()"></div>
		<div class="theme-bg" id="bg">
			<div class="fire-box">
				<div class="fire-item item1">
				</div>
				<div class="fire-item item2"></div>
				<div class="fire-item item3"></div>
				<div class="fire-item item4"></div>
				<div class="fire-item item5"></div>
			</div>
			<div class="text-box"></div>
			<div v-if="act_status == '1'" class="timer-count">已点亮<span class="num">{{totalSakuraNum}}</span>场花火，距分钱还剩<span class="num">{{act_remain_day}}</span>天</div>
			<div v-else class="timer-count">{{act_text}}</div>
		</div>
		
		<div class="reel-box">
			<div class="my-sakura-box" >
				<div>点亮的花火</div>
				<div class="my-sakura">
					<div class="my-sakura-new"></div>
					<div>X{{sakura_H_num || 0}}</div>
				</div>
			</div>
			<form :report-submit="form_id" @submit="gather" >
				<button class="w-sakura" @click="showSakuraW()" form-type="submit">
					<div class="count-box">
						万能花火
					</div>
					<div class="w-count">{{sakura_W_num}}</div>
				</button>
			</form>
			<div class="flower-box">
				<div class="right">
					<form :report-submit="form_id" @submit="gather" >
						<button class="flower-item flower-item-dyh" :class="{'gray': sakura_C_num == '0'}" @click="showSakuraDetail('sakura_c','洞爷湖花火大会','全国花火競技大会「洞爷湖の花火」')">
							<div class="tag" :class="{'gray': sakura_C_num == '0'}" style="left:50%;top: 80%">
								洞爷湖花火大会
								<div v-if="sakura_C_num > 0" class="num-box">{{sakura_C_num}}</div>
							</div>
							<div class="fire-ani-box" v-if="sakura_C_num != '0'">
								<div class="firecracker" style="left:55%;top: 40%">
									<div class="ani" :class="{'ani-delay': sakura_C_num > 0 }"></div>
									<div class="boom" :class="{'ani-delay': sakura_C_num > 0 }"></div>
								</div>
							</div>
						</button>
					</form>
				</div>
				<div class="center">
					<form :report-submit="form_id" @submit="gather" @click="showSakuraDetail('sakura_d','大曲花火大会','全国花火競技大会「大曲の花火」')">
						<button class="flower-item flower-item-dq" :class="{'gray': sakura_D_num == '0'}">
							<div class="tag" :class="{'gray': sakura_D_num == '0'}" style="left:80%;top: 50%">
								大曲花火大会
								<div v-if="sakura_D_num > 0" class="num-box">{{sakura_D_num}}</div>
							</div>
							<div class="fire-ani-box" v-if="sakura_D_num != '0'">
								<div class="firecracker" style="left:55%;top: 40%">
									<div class="ani"></div>
									<div class="boom"></div>
								</div>
							</div>
						</button>
					</form>
					<form :report-submit="form_id" @submit="gather" >
						<button class="flower-item flower-item-db" :class="{'gray': sakura_E_num == '0'}" @click="showSakuraDetail('sakura_e','大阪天神祭','全国花火競技大会「大阪の花火」')">
							<div class="tag" :class="{'gray': sakura_E_num == '0'}" style="left:60%;top: -100%">
								大阪天神祭
								<div v-if="sakura_E_num > 0" class="num-box" style="right: auto;left:0">{{sakura_E_num}}</div>
							</div>
							<div class="fire-ani-box" v-if="sakura_E_num != '0'">
								<div class="firecracker" style="left:70%;top: 20%">
									<div class="ani"></div>
									<div class="boom"></div>
								</div>
							</div>
						</button>
					</form>
					<form :report-submit="form_id" @submit="gather" >
						<button class="flower-item flower-item-tf" :class="{'gray': sakura_B_num == '0'}" @click="showSakuraDetail('sakura_b','土浦花火大会','全国花火競技大会「土浦の花火」')">
							<div class="tag" :class="{'gray': sakura_B_num == '0'}" style="left:30%;top: 80%">
								土浦花火大会
								<div v-if="sakura_B_num > 0" class="num-box">{{sakura_B_num}}</div>
							</div>
							<div class="fire-ani-box" v-if="sakura_B_num != '0'">
								<div class="firecracker" style="left:25%;top: 40%">
									<div class="ani" :class="{'ani-delay': sakura_B_num > 0 }"></div>
									<div class="boom" :class="{'ani-delay': sakura_B_num > 0 }"></div>
								</div>
							</div>
						</button>
					</form>
				</div>
				<div class="left">
					<form :report-submit="form_id" @submit="gather" >
						<button class="flower-item flower-item-zhc" :class="{'gray': sakura_A_num == '0'}" @click="showSakuraDetail('sakura_a','筑后川花火大会','全国花火競技大会「筑后川の花火」')">
							<div class="tag" :class="{'gray': sakura_A_num == '0'}" style="left:10%;top: 80%">
								筑后川花火大会
								<div v-if="sakura_A_num > 0" class="num-box">{{sakura_A_num}}</div>
							</div>
							<div class="fire-ani-box" v-if="sakura_A_num != '0'">
								<div class="firecracker" style="left:15%;top: 20%">
									<div class="ani" :class="{'ani-delay': sakura_A_num > 0 }"></div>
									<div class="boom" :class="{'ani-delay': sakura_A_num > 0 }"></div>
								</div>
							</div>
						</button>
					</form>
				</div>
				<form :report-submit="form_id" @submit="gather" >
					<button class="mix-btn" form-type="submit" @click="showComposeAni()">
						<div class="wave">
							<div class="wave-pos" :style="{'transform': 'translateY(' + (15*(-is_compose)) + 'px)'}">
								<div class="wave-pos-before"></div>
								<div class="wave-pos-after"></div>
							</div>
						</div>
						<div class="mix-btn-text">点亮花火</div>
					</button>
				</form>
			</div>
			<div class="rest-count">
				今日剩余收集次数<span>{{rest_count || 0}}</span>/{{total_count || 9}}
			</div>
			<form :report-submit="form_id" @submit="gather" >
				<button class="lottery-btn" form-type="submit" v-if="act_status == '1'" @click="lotterySakura()">
					收集花火
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
				待开奖
			</div>
			<div class="rec-btn" @click="showGiftRec()">
				赠领记录
			</div>
		</div>
		<div class="task-box">
			<div class="task-title">
				做任务获得点亮机会
			</div>
			<div class="task-item" v-for="item in taskList" :key="item.task_id">
				<div>{{item.name}}</div>
				<div class="task-item-img">
					<div class="num">{{item.count}}次</div>
				</div>
				<form :report-submit="form_id" @submit="gather" >
					<button v-if="item.status == '0'" form-type="submit" class="task-item-btn receive" @click="getTask(item.task_id)">
						领取
					</button>
				</form>
				<div v-if="item.status == '1'" class="task-item-btn done">
					已完成
				</div>
				<form :report-submit="form_id" @submit="gather" >
					<div v-if="item.status == '-1'">
						<button v-if="item.task_id == '2'" class="task-item-btn" open-type="share" :data-type="1" @click="doTask2()">
							去分享
						</button>
						<button v-if="item.task_id != '2'"  class="task-item-btn" form-type="submit" @click="toFinishTask(item.task_id,item.page_id)">
							去完成
						</button>
					</div>
				</form>
			</div>
			<div class="task-item">
				<div class="suc-box">
					<div class="suc-box-right">
						邀请新朋友加入豌豆得<span>万能花火</span>
					</div>
				</div>
				<!-- <div class="task-item-img" @click="showSakuraW()">
					<div v-if="sakura_W_num > 0" class="num">{{sakura_W_num}}</div>
					<div v-else class="num">3</div>
				</div> -->
				<form :report-submit="form_id" @submit="gather" >
					<button class="task-item-btn" form-type="submit" @click="showinviteSakuraAll()">去邀请</button>
				</form>
			</div>
		</div>
		<div class="brand-box" v-if="topRankList && topRankList.length > 0 ">
			<div class="task-title">
				点亮成就榜
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
							<div>已点亮庆生花火<span class="flower">{{userRankList.total}}</span>次</div>
							<div class="time">{{userRankList.last_time}}</div>
						</div>
					</div>
				</div>
				<swiper class="brand-box-top" vertical autoplay circular>
					<swiper-item style="height: 34px;" v-for="(swiperitem, swiperindex) in topRankList" :key="swiperindex">
						<div class="brand-box-top-item" v-for="(item, index) in swiperitem" :key="index">
							<div class="rank">
								<div class="last">{{5*swiperindex + index+1}}</div>
							</div>
							<div class="img-box">
								<img :src="item.imgurl" alt="">
								<div class="name">{{item.nickname}}</div>
							</div>
							<div class="flower-box">
								<div>已点亮庆生花火<span class="flower">{{item.total}}</span>次</div>
								<div class="time">{{item.last_time}}</div>
							</div>
						</div>
					</swiper-item>
				</swiper>
			</div>
		</div>
		<div v-if="buoy_ad_info.ad_img != ''"  class="ad-img-fixed" :class="{'scrolling': isScrolling}" @click="toFixedCard()">
			<img :src="buoy_ad_info.ad_img" alt="">
		</div>
		<div id="mask" v-if="maskShow">
			<div class="compose-box" v-if="showAlert == 'compose'">
				<div class="compose-ani-before"></div>
				<div class="compose-ani"></div>
				<div class="compose-ani2-before"></div>
				<div class="compose-ani-2"></div>
				<div class="compose-ani3-before"></div>
				<div class="compose-ani-3"></div>
				<div class="compose-ani4-before"></div>
				<div class="compose-ani-4"></div>
				<div class="compose-ani5-before"></div>
				<div class="compose-ani-5"></div>
			</div>
			<!-- 点击**樱花瓣弹框 -->
			<div class="to-alert-box" v-if="showAlert == 'sakuraDetail'">
				<div class="colse" @click="closeAlert()"></div>
				<div class="sakura-text">
					<div class="name">{{sakuraDetailName}}</div>
					<div class="poetry">{{sakuraDetailPoetry}}</div>
				</div>
				<img v-if="sakuraDetailKey == 'sakura_a'" class="mysakura" src="https://s4.wandougongzhu.cn/s/3a/zhc_8eeb51.jpg">
				<img v-if="sakuraDetailKey == 'sakura_b'" class="mysakura" src="https://s1.wandougongzhu.cn/s/92/tf_61b463.jpg">
				<img v-if="sakuraDetailKey == 'sakura_c'" class="mysakura" src="https://s3.wandougongzhu.cn/s/9f/dyh_984083.jpg">
				<img v-if="sakuraDetailKey == 'sakura_d'" class="mysakura" src="https://s3.wandougongzhu.cn/s/72/dq_196ee4.jpg">
				<img v-if="sakuraDetailKey == 'sakura_e'" class="mysakura" src="https://s3.wandougongzhu.cn/s/b9/db_d1cdb7.jpg">
				<div class="mysakura-tips">
					<p>每天首次赠送可获得一次抽花火的机会</p>
					<p>取消分享也会扣除花火，一定完成分享哦~</p>
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
					<div class="congratulation">恭喜您~获得了</div>
					<div class="name">{{lottery_res.sakura_name}}</div>
				</div>
				<div class="getsakura" 
					:class="{'zhc':lottery_res.sakura_key == 'sakura_a','tf':lottery_res.sakura_key == 'sakura_b','dyh':lottery_res.sakura_key == 'sakura_c','dq':lottery_res.sakura_key == 'sakura_d','db':lottery_res.sakura_key == 'sakura_e',}">

				</div>
				<div class="getsakura-text" v-if="lottery_res.sakura_key == 'sakura_a'">
					即将迎接第360年历史了，始终是九州人气花火期待度排名第一的筑后川花火大会，起源来自水天宫的奉纳祭祀，是一场结合平安祈福的烟火节庆。
				</div>
				<div class="getsakura-text" v-if="lottery_res.sakura_key == 'sakura_b'">
					土浦全国烟火大会是可自由入场的竞赛大会，是日本三大烟花大会之一，也是日本全国人气数一数二的烟花比赛。
				</div>
				<div class="getsakura-text" v-if="lottery_res.sakura_key == 'sakura_c'">
					洞爷湖花火大会是日本举办期间最长的烟花大会，烟火是在行驶在湖面的船隻上释放的，是夏天来北海道不可或缺的活动。
				</div>
				<div class="getsakura-text" v-if="lottery_res.sakura_key == 'sakura_d'">
					秋田县大仙市举办的大曲烟火大会，是从日本全国各地选拔出来的烟火师亲手施放高空烟火的烟火竞赛大会，是全日本最具有代表性的花火大会之一。
				</div>
				<div class="getsakura-text" v-if="lottery_res.sakura_key == 'sakura_e'">
					具有1000多年历史的大坂天神祭是日本三大祭典之一，祭奉日本的「学问和艺术之神」棺原道真。
				</div>
				<form :report-submit="form_id" @submit="gather" >
					<button class="mysakura-btn" form-type="submit" @click="closeAlert()">
						确定
					</button>
				</form>
			</div>
			 <!-- 恭喜获得万能樱 -->
			 <!-- sakuraAll -->
			<div class="get-alert-box" v-if="showAlert == 'sakuraAll'">
				<div class="colse" @click="closeAlert()"></div>
				<div class="mysakura-text">
					<div class="congratulation">恭喜你，获得了</div>
					<div class="name">万能花火</div>
				</div>
				<div class="getsakura universal"></div>
				<div class="getsakura-text" style="text-align: center;">
					万能花火可兑换任意地区花火
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
					<div class="invite-title">邀请好友注册得万能花火</div>
					<div>万能花火可兑换任意地区花火</div>
				</div>
				<img class="getsakura invite-sakura" src="https://s3.wandougongzhu.cn/s/8b/_830d8b.jpg">
				<form :report-submit="form_id" @submit="gather" >
					<button class="invite-btn" form-type="submit" open-type="share" :data-type="2">
						去邀请
					</button>
				</form>
				<div class="universal-tips">花火在好友验证手机号后发放</div>
			</div>
			<!-- 万能樱兑换 -->
			<!-- sakuraAllChange -->
			<div class="get-alert-box" v-if="showAlert == 'sakuraAllChange'">
				<div class="colse" @click="closeAlert()"></div>
				<div class="mysakura-text">
					<div class="universal-compose">请选择要兑换的花火</div>
					<div class="universal-tips">使用1个万能花火可以兑换任意地区花火</div>
				</div>
				<div class="flower-box universal-flower">
					<div class="right">
						<form :report-submit="form_id" @submit="gather" >
							<button class="flower-item flower-item-dyh" :class="{'gray': sakura_whitch_choosed != 'sakura_c'}" @click="chooseChangeSakura('sakura_c')">
								<div class="tag" :class="{'gray': sakura_whitch_choosed != 'sakura_c'}" style="left:50%;top: 80%">
									洞爷湖花火大会
									<div v-if="sakura_C_num > 0" class="num-box">{{sakura_C_num}}</div>
								</div>
							</button>
						</form>
					</div>
					<div class="center">
						<form :report-submit="form_id" @submit="gather" >
							<button class="flower-item flower-item-dq" :class="{'gray': sakura_whitch_choosed != 'sakura_d'}" @click="chooseChangeSakura('sakura_d')">
									<div class="tag" :class="{'gray': sakura_whitch_choosed != 'sakura_d'}" style="left:80%;top: 50%">
									大曲花火大会
									<div v-if="sakura_D_num > 0" class="num-box">{{sakura_D_num}}</div>
								</div>
							</button>
						</form>
						<form :report-submit="form_id" @submit="gather" >
							<button class="flower-item flower-item-db" :class="{'gray': sakura_whitch_choosed != 'sakura_e'}" @click="chooseChangeSakura('sakura_e')">
								<div class="tag" :class="{'gray': sakura_whitch_choosed != 'sakura_e'}" style="left:60%;top: -100%">
									大阪天神祭
									<div v-if="sakura_E_num > 0" class="num-box">{{sakura_E_num}}</div>
								</div>
							</button>
						</form>
						<form :report-submit="form_id" @submit="gather" >
							<button class="flower-item flower-item-tf" :class="{'gray': sakura_whitch_choosed != 'sakura_b'}" @click="chooseChangeSakura('sakura_b')">
								<div class="tag" :class="{'gray': sakura_whitch_choosed != 'sakura_b'}" style="left:30%;top: 80%">
									土浦花火大会
									<div v-if="sakura_B_num > 0" class="num-box">{{sakura_B_num}}</div>
								</div>
							</button>
						</form>
					</div>
					<div class="left">
						<form :report-submit="form_id" @submit="gather" >
							<button class="flower-item flower-item-zhc" :class="{'gray': sakura_whitch_choosed != 'sakura_a'}" @click="chooseChangeSakura('sakura_a')">
								<div class="tag" :class="{'gray': sakura_whitch_choosed != 'sakura_a'}" style="left:20%;top: 50%">
									筑后川花火大会
									<div v-if="sakura_A_num > 0" class="num-box">{{sakura_A_num}}</div>
								</div>
							</button>
						</form>
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
			 <!-- // todo,赠送的时候带sakura_key -->
			<div class="get-alert-box" v-if="showAlert == 'inviteShareSakura'">
				<div class="colse" @click="closeAlert()"></div>
				<div class="mysakura-text">
					<div class="congratulation">好友<span>{{inviteUser}}</span>送你一个</div>
					<div class="name">{{inviteShareSakuraName}}</div>
				</div>
				<div class="getsakura" 
					:class="{'zhc':inviteShareSakuraKey == 'sakura_a','tf':inviteShareSakuraKey == 'sakura_b','dyh':inviteShareSakuraKey == 'sakura_c','dq':inviteShareSakuraKey == 'sakura_d','db':inviteShareSakuraKey == 'sakura_e'}">
				</div>
				<div class="getsakura-text" v-if="inviteShareSakuraKey == 'sakura_a'">
					即将迎接第360年历史了，始终是九州人气花火期待度排名第一的筑后川花火大会，起源来自水天宫的奉纳祭祀，是一场结合平安祈福的烟火节庆。
				</div>
				<div class="getsakura-text" v-if="inviteShareSakuraKey == 'sakura_b'">
					土浦全国烟火大会是可自由入场的竞赛大会，是日本三大烟花大会之一，也是日本全国人气数一数二的烟花比赛。
				</div>
				<div class="getsakura-text" v-if="inviteShareSakuraKey == 'sakura_c'">
					洞爷湖花火大会是日本举办期间最长的烟花大会，烟火是在行驶在湖面的船隻上释放的，是夏天来北海道不可或缺的活动。
				</div>
				<div class="getsakura-text" v-if="inviteShareSakuraKey == 'sakura_d'">
					秋田县大仙市举办的大曲烟火大会，是从日本全国各地选拔出来的烟火师亲手施放高空烟火的烟火竞赛大会，是全日本最具有代表性的花火大会之一。
				</div>
				<div class="getsakura-text" v-if="inviteShareSakuraKey == 'sakura_e'">
					具有1000多年历史的大坂天神祭是日本三大祭典之一，祭奉日本的「学问和艺术之神」棺原道真。
				</div>
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
					<div class="name">手慢了，花火已被别人领取了～</div>
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
					<div class="name">花火已扣除，快去分享给好友吧！</div>
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
let ch = '828_huahuodahui_mp';

export default {
	data() {
		return {
			form_id:true,
			user_id: '',
			userInfo: {},
			flowerStatus: '0',
			status: '-1',
			text: '',
			sakura_A_num: 0, //筑后川花火大会
			sakura_B_num: 0, //土浦花火大会
			sakura_C_num: 0, //洞爷湖花火大会 
			sakura_D_num: 0, //大曲花火大会
			sakura_E_num: 0, //大阪天神祭
			sakura_W_num: 0, //万能花火数量
			sakura_G_num: 0, //赠送花火数量
			sakura_H_num: 0, //合成花火数量
			is_compose: 0, //有几种类型花火 决定是否可以合成
			rest_count: 0, //剩余抽奖次数
			total_count: 9, //今日可抽总次数
			lottery_res: {}, //抽取花火结果
			maskShow: false, //蒙层
			taskList: [],
			totalSakuraNum: 0,
			lastSakuraNum: 500000,
			progressSakura: 0, //集花火进度0-5代表0w-50w
			restDay: 10,
			restText: '',
			lock: false,
			sakuraDetailKey: 'sakura_a',
			sakuraDetailName: '筑后川花火大会',
			sakuraDetailPoetry: '築後川花火大會',
			shareImg: 'https://s1.wandougongzhu.cn/s/81/_9163d6.jpg', //分享图
			shareImgBtn: {
				'sakura_a': 'https://s.wandougongzhu.cn/s/16/-_b46163.jpg',
				'sakura_b': 'https://s3.wandougongzhu.cn/s/58/-_452eb2.jpg',
				'sakura_c': 'https://s1.wandougongzhu.cn/s/c4/-_2b2c54.jpg',
				'sakura_d': 'https://s5.wandougongzhu.cn/s/e6/-_405b31.jpg',
				'sakura_e': 'https://s4.wandougongzhu.cn/s/a5/-_0732fe.jpg'
			},//分享花火给好友图了list
			shareSakura: 'sakura_a',
			sakura_All_num: 0, //万能花火数量
			sakura_whitch_choosed: '',
			exchange_sakura_key: '', //要兑换的花火
			inviteCount: 0, //邀请好友数量
			ruleShowMore: false,
			ruleShowText: '展开更多',
			giftRecList: [], //赠领记录
			invite_sakura: '', //通过邀请来领取的花火key
			invite_user_id: '', //邀请人id
			option: '',
			inviteUser: '', //好友昵称
			inviteShareSakuraName: '', //好友送的**盈
			inviteShareSakuraKey: '', //好友送的**盈
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
			cloundShareSakuraInfo: {}, //云控分享花火
			topRankList: [], //排行榜数据
			userRankList: {}, //当前用户的排行数据
			showFaceTime: '0', //是否显示山下久智FaceTime
			pageId: 19767, //活动规则卡片页id
			isScrolling: false,
			logCommonParam: {
				ns: '828_huahuodahui_mp',
				w: '',
				open_id: '',
				devtype: 'mp',
				ch: ch,
			},
		};
	},
	onLoad() {
		wx.hideShareMenu();
		wx.setStorage({ key: 'ch', data: ch });
		WMP.globalData.ch = ch;
		//浏览打点
		Net.newLog(
			{
				mt: 'huahuodahui_uv',
				ivt: this.option.user_id || '',
			},
			this.logCommonParam,
		);
		this.option = this.$root.$mp.query;
		console.log(this.$root.$mp);
		if (!WMP.globalData.userInfo || !WMP.globalData.userInfo.user_id) {
			let is_first = wx.getStorageSync('is_first_access');
			if(is_first == '0'){
				console.log(is_first);
			}else{
				Net.newLog(
					{
						mt: 'huahuodahui_access',
					},
					this.logCommonParam,
				);
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
						title: '不能领取自己分享的花火～',
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
	onUnload() {
	},
	onPageScroll(e) {
		let scrollTopNow =  e.scrollTop;
		this.isScrolling = true;
		let timer = setTimeout(()=> {
			if(scrollTopNow === e.scrollTop) {
				this.isScrolling = false;
				console.log('滚动结束');
				clearTimeout(timer);
			}
		},300);
	},
	onShow() {
		this._getUserActInfo();
	},
	onShareAppMessage (res) {
		let self = this;
		this.closeAlert();
		if (res.from == 'button' && res.target.dataset.type == '0') {
			if (res.target.dataset.sakuraid) {
				Net.newLog(
					{
						mt: 'huahuodahui_share_flower',
					},
					this.logCommonParam,
				);
				console.log('data-sakuraid='+ res.target.dataset.sakuraid);
				return {
					title: '送你一朵'+res.target.dataset.sakuraname + this.cloundShareSakuraInfo.title,
					path: '/pages/fireworks/main?sakura_key=' + res.target.dataset.sakurakey +'&user_id=' + this.user_id +"&sakura_id=" + res.target.dataset.sakuraid + '&ch=' + ch,
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
				Net.newLog(
					{
						mt: 'huahuodahui_share_flower',
					},
					this.logCommonParam,
				);
				return {
					title: '送你一朵'+this.sakuraDetailName + this.cloundShareSakuraInfo.title,
					path: '/pages/fireworks/main?sakura_key=' + this.sakuraDetailKey +'&user_id=' + this.user_id +"&sakura_id=" + this.sakura_id + '&ch=' + ch,
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
					path: '/pages/fireworks/main?user_id=' + this.user_id + '&ch=' + ch,
					imageUrl: shareImg,
					success: function (res) {
						Net.newLog(
							{
								mt: 'huahuodahui_share_act',
							},
							self.logCommonParam,
						);
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
					Net.newLog(
						{
							mt: 'huahuodahui_task_2',
						},
						self.logCommonParam,
					);
					return {
						title: this.cloundShareActInfo.title + this.act_text + '!',
						path: '/pages/fireworks/main?user_id=' + this.user_id + '&ch=' + ch,
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
					Net.newLog(
						{
							mt: 'huahuodahui_share_act',
						},
						self.logCommonParam,
					);
					return {
						title: this.cloundShareActInfo.title + this.act_text + '!',
						path: '/pages/fireworks/main?user_id=' + this.user_id + '&ch=' + ch,
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
		
		getRandom(min, max) {
			return Math.floor((max - min) * Math.random()) + min;
		},
		goCash() {
			WMP.checkAuthPromise(this.$root.$mp.page).then(() => {
				wx.navigateTo({ 
					url: '/pages/tocash/main' 
				});
			})
		},
		doTask2() {
			Net.newLog(
				{
					mt: 'huahuodahui_task_2',
				},
				this.logCommonParam,
			);
			this.shareActivity();
			this.getUserActInfo();
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
			Net.newLog(
				{
					mt: 'huahuodahui_go_ad',
				},
				this.logCommonParam,
			);
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
				scene_val: 'huahuodahui',
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
					let tmpResult = [];
					for(let i=0,len=res.data.top_list.length;i<len;i+=5){
						tmpResult.push(data.slice(i,i+5));
					}
					this.topRankList = tmpResult;
					this.userRankList = res.data.user_seq || {};
					this.sakura_A_num = infoList.sakura_a;
					this.sakura_B_num = infoList.sakura_b;
					this.sakura_C_num = infoList.sakura_c;
					this.sakura_D_num = infoList.sakura_d;
					this.sakura_E_num = infoList.sakura_e;
					this.sakura_W_num = infoList.sakura_w;
					this.sakura_H_num = parseInt(infoList.sakura_h);
					this.sakura_G_num = infoList.sakura_g;
					this.is_compose = Number(infoList.sakura_a > 0) + Number(infoList.sakura_b > 0) + Number(infoList.sakura_c > 0) + Number(infoList.sakura_d > 0)+ Number(infoList.sakura_e > 0);
					this.rest_count = infoList.residue_lottery_count;
					this.total_count = infoList.day_total;
					// this.user_id = infoList.user_id;
					this.totalSakuraNum = res.data.h_sakura_count;
					this.inviteCount = res.data.info.invite_count;
					this.inviteUser = res.data.gift_sakura.gift_user_name;
					this.inviteShareSakuraName = res.data.gift_sakura.sakura_name;
					this.inviteShareSakuraKey = res.data.gift_sakura.sakura_key;
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
						Net.newLog(
							{
								mt: 'huahuodahui_get_flower_self',
							},
							this.logCommonParam,
						);
						wx.showToast({
							title: '不能领取自己分享的花火～',
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
								Net.newLog(
									{
										mt: 'huahuodahui_get_flower_success',
									},
									this.logCommonParam,
								);
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
						Net.newLog(
							{
								mt: 'huahuodahui_get_flower_fail',
							},
							this.logCommonParam,
						);
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
				Net.newLog(
					{
						mt: 'huahuodahui_access1',
					},
					this.logCommonParam,
				);
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
						let tmpResult = [];
						for(let i=0,len=res.data.top_list.length;i<len;i+=5){
							tmpResult.push(data.slice(i,i+5));
						}
						this.topRankList = tmpResult;
						this.userRankList = res.data.user_seq;
						this.sakura_A_num = infoList.sakura_a;
						this.sakura_B_num = infoList.sakura_b;
						this.sakura_C_num = infoList.sakura_c;
						this.sakura_D_num = infoList.sakura_d;
						this.sakura_E_num = infoList.sakura_e;
						this.sakura_W_num = infoList.sakura_w;
						this.sakura_H_num = parseInt(infoList.sakura_h);
						this.sakura_G_num = infoList.sakura_g;
						this.is_compose = Number(infoList.sakura_a > 0) + Number(infoList.sakura_b > 0) + Number(infoList.sakura_c > 0) + Number(infoList.sakura_d > 0)+ Number(infoList.sakura_e > 0);
						this.rest_count = infoList.residue_lottery_count;
						this.total_count = infoList.day_total;
						// this.user_id = infoList.user_id;
						this.totalSakuraNum = res.data.h_sakura_count;
						this.inviteCount = res.data.info.invite_count;
						this.inviteUser = res.data.gift_sakura.gift_user_name;
						this.inviteShareSakuraName = res.data.gift_sakura.sakura_name;
						this.inviteShareSakuraKey = res.data.gift_sakura.sakura_key;
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
		showHaveDone() {
			this.maskShow = true;
			this.showAlert = 'showHaveDone';
			Net.newLog(
				{
					mt: 'huahuodahui_get_flower_fail',
				},
				this.logCommonParam,
			);
		},
		showSakuraDetail(key, name, poetry) {
			if (this.act_status == '1') {
				this.sakuraDetailKey = key;
				this.sakuraDetailName = name;
				this.sakuraDetailPoetry = poetry;
				
				this.maskShow = true;
				this.showAlert = 'sakuraDetail';
			} else {
				wx.showToast({
					title: '抽花火已结束',
					icon: 'error',
					duration: 2000
				});
			}
		},
		showComposeAni() {
			if (this.is_compose == '5') {
				Net.get('Sakura.userComposeSakura', {
					data: {
						user_id: this.user_id
					}
				}).then(res=>{
					if(res.errno=='0') {
						this.maskShow = true;
						this.showAlert = 'compose';
						setTimeout(()=>{
							this.showAlert = '';
							this.maskShow = false;
						},3500);
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
					title: '花火数量不足～',
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
						title: '万能花火不足～',
						icon: 'error',
						duration: 1500,
					})
				}
			} else {
				wx.showToast({
					title: '请选择一个花火',
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
					Net.newLog(
						{
							mt: 'huahuodahui_task_' + parseInt(paramTask),
						},
						this.logCommonParam,
					);
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
				Net.newLog(
					{
						mt: 'huahuodahui_task_' + parseInt(paramTask),
					},
					this.logCommonParam,
				);
				if (task_id == 3) {
					if (this.sakura_A_num == '0' && this.sakura_B_num == '0' && this.sakura_C_num == '0' && this.sakura_D_num == '0' && this.sakura_E_num == '0') {
						wx.showToast({
							title: '当前没有花火～',
							icon: 'none',
							duration: 1500,
						});
					} else {
						wx.navigateTo({
							url: '/pages/togift/main',
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
.ad-img-fixed {
	position: fixed;
	width: 50px;
	height: 50px;
	border-radius: 50%;
	right: 30px;
	bottom: 50px;
	z-index: 2;
}
.ad-img-fixed img {
	width: 100%;
	height: 100%;
}
.ad-img-fixed.scrolling {
	opacity: 0.5;
}
.invite-text {
	font-size: 12px;
	color: rgb(67, 67, 67);
	margin: 30px auto 20px auto;
}
.invite-text .invite-title {
	font-size: 15px;
}
.my-sakura-box {
	position: absolute;
	width: 130px;
	overflow: hidden;
	font-size: 16px;
	line-height: 25px;
	color: #000;
	font-weight: bold;
	text-align: left;
	margin: 30px auto 0 15px;
}

.my-sakura {
	width: 100%;
	display: flex;
	flex-wrap: wrap;
  color: rgb(214, 35, 35);
}
.my-sakura-new {
	width: 20px;
	height: 20px;
	margin: 2px 3px 0 0;
	background: url('https://s.wandougongzhu.cn/s/7a/513_d24f95.png') no-repeat;
	background-size: cover;
}
.w-sakura {
	position: absolute;
	right: 10px;
	top: 12px;
	width: 31px;
	height: 92px;
	font-weight: bold;
	background: url('https://s3.wandougongzhu.cn/s/f0/2x_3ae473.png') no-repeat;
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
	margin: 15px 5px 0 5px;
	text-align: center;
	color: #fff;
	font-size: 12px;
	line-height: 14px;
	white-space: wrap;
}
.w-sakura .w-count {
	margin: 3px 10px 0 10px;
	line-height: 16px;
	color: #fff;
	font-size: 16px;
	text-align: center;
	display: flex;
	justify-content: center;
}
.timer-count {
	width: 270px;
	height: 35px;
	line-height: 35px;
	margin: 5px auto 0 auto;
	font-size: 13px;
	font-weight: bold;
	color: #000;
	text-align: center;
	background: url(https://s3.wandougongzhu.cn/s/91/_ebc44f.png) no-repeat;
	background-size: contain;
	background-position: center;
}
.timer-count .num {
	color: #d52223;
	margin: 0 2px;
}
.colse {
	position: absolute;
	top: 15px;
	right: 15px;
	width: 20px;
	height: 20px;
	background: url('https://s.wandougongzhu.cn/s/eb/close_a4ff2d.png') no-repeat;
	z-index: 2;
	background-size: contain;
}
.num-box, .task-item-img .num, .have-flower-num {
	width: 20px;
	height: 20px;
	text-align: center;
	line-height: 20px;
	color: #fff;
	font-size:14px;
	position:absolute;
	right:0;
	background: url('https://s5.wandougongzhu.cn/s/5e/3_41b2d3.png') no-repeat;
	background-size: cover;
}
.task-item-img .num {
	width: 25px;
	height: 25px;
	background: url('https://s4.wandougongzhu.cn/s/5f/2_5a2e1c.png') no-repeat;
	background-size: cover;
}
.to-alert-box,.get-alert-box {
	position: absolute;
	left: 50%;
	top: 50%;
	transform: translate(-50%,-50%);
	width: 298px;
	height: 382px;
	font-size: 14px;
	font-weight: normal;
	text-align: center;
	background: url('https://s3.wandougongzhu.cn/s/cc/alert_7c4ab3.png') no-repeat;
	background-size: 100% 100%;
	z-index: 3;
}
.suc-alert-box {
	height: 160px;
	background: url('https://s4.wandougongzhu.cn/s/a2/alert_s_f4973c.png') no-repeat;
	background-size: 100% 100%;
}
.suc-alert-box  .mysakura-text .name {
	font-size: 12px;
	margin-top: 20px;
}
.universal-compose {
	font-size: 20px;
	font-weight: bold;
  color: rgb(213, 34, 35);
}
.sakura-text {
	text-align: center;
}
.universal-tips {
	font-size: 12px;
	line-height: 20px;
}
.congratulation {
	font-size: 14px;
	line-height: 25px;
	font-weight: bold;
}
.gift-res-title {
	font-size: 16px;
	font-weight: bold;
	margin-top: 25px;
	background: url(https://s1.wandougongzhu.cn/s/96/dot_83dfe9.png) no-repeat;
	background-size: 140px auto;
	background-position: center;
}
.gift-res-content {
	height: 270px;
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
	font-size: 10px;
	color: #fff;
	text-align: center;
	line-height: 20px;
	background: url('https://s5.wandougongzhu.cn/s/09/_ad9e3d.png') no-repeat;
	background-size: 100% 100%;
}
.gift-res-item .time {
	line-height: 20px;
	color: rgb(153, 153, 153);
}
.gift-res-item-null {
	font-size: 12px;
	margin: 50px auto;
	font-weight: bold;
}
.mysakura-text {
	margin-top: 20px;
}
.mysakura-text .name{
	font-size: 20px;
	line-height: 22px;
	font-weight: bold;
  color: rgb(213, 34, 35);
}
.mysakura-text-done {
	margin-top: 60px;
	font-weight: bold;
}
.sakura-text .poetry {
	font-weight: bold;
  color: rgb(18, 20, 59);
	font-size: 12px;
	line-height: 20px;
}
.sakura-text .name {
	margin-top: 20px;
	font-size: 20px;
	line-height: 22px;
	font-weight: bold;
  color: rgb(213, 34, 35);
}
.mysakura,.getsakura{
	width: 260px;
	height: 177px;
	position: relative;
	margin: 10px auto;
}
.mysakura.tf,.getsakura.tf {
	background: url('https://s1.wandougongzhu.cn/s/92/tf_61b463.jpg') no-repeat;
	background-size: cover;
}
.mysakura.dq,.getsakura.dq {
	background: url('https://s3.wandougongzhu.cn/s/72/dq_196ee4.jpg') no-repeat;
	background-size: cover;
}
.mysakura.zhc,.getsakura.zhc {
	background: url('https://s4.wandougongzhu.cn/s/3a/zhc_8eeb51.jpg') no-repeat;
	background-size: cover;
}
.mysakura.dyh,.getsakura.dyh {
	background: url('https://s3.wandougongzhu.cn/s/9f/dyh_984083.jpg') no-repeat;
	background-size: cover;
}
.mysakura.db,.getsakura.db {
	background: url('https://s3.wandougongzhu.cn/s/b9/db_d1cdb7.jpg') no-repeat;
	background-size: cover;
}
.mysakura.universal,.getsakura.universal {
	background: url('https://s1.wandougongzhu.cn/s/fe/_28e26d.jpg') no-repeat;
	background-size: cover;
}
.getsakura-text {
	width: 260px;
	margin: 0 auto;
	text-align: left;
	font-size: 12px;
	line-height: 18px;
  color: rgb(18, 20, 59);
}
.mysakura-tips {
	width: 100%;
	position: absolute;
	color: rgb(111, 111, 111);
	bottom: 70px;
	font-size: 12px;
	
	text-align: center;
	font-weight: normal;
}
.mysakura-btn {
	position: absolute;
	left: 50%;
	transform: translate(-50%,0);
	bottom: 16px;
	width: 85px;
	height: 34px;
	line-height: 34px;
	font-size: 12px;
	color: #fff;
	background: url('https://s5.wandougongzhu.cn/s/09/_ad9e3d.png') no-repeat;
	background-size: 100% 100%;
	margin: 0 auto;
	border-radius: 0;
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
	display: block;
	position: absolute;
	right: 5px;
	top: 2px;
	width: 32px;
	height: 40px;
	background: url('https://s4.wandougongzhu.cn/s/5e/_9d0db2.png') no-repeat;
	background-size: contain;
	color: #FFFFFF;
	z-index: 1;
}
.rec-btn {
	position: absolute;
	left: 15px;
	bottom: 20px;
	display: inline;
	font-size: 14px;
	text-decoration: underline;
	color: #000;
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
	width: 100%;
	height: 100%;
	text-align: center;
	padding: 0;
	margin: 0;
	padding-bottom: 60px;
	background-color: #14143c;
}
.theme-bg {
	position: relative;
	width: 100%;
	height: 170px;
	background: url(https://s5.wandougongzhu.cn/s/7c/_3be6c4.png) no-repeat;
	background-size: cover;
	font-size: 30px;
	color: #fff;
	overflow: hidden;
	text-align: center;
}
.theme-bg .fire-box {
	width: 100%;
	position: relative;
}
.fire-box .fire-item {
	position: absolute;
	width: 80px;
	height: 73px;
	background: url(https://s1.wandougongzhu.cn/s/56/_584e00.png) no-repeat;
	background-size: contain;
}
.fire-item.item1 {
	top: -30px;
	left: -30px;
	opacity: 0.6;
	/* animation: breath 1s ease infinte;
	-webkit-animation: breath 1s ease infinite; */
}
.fire-item.item2 {
	top: -20px;
	left: 70px;
	opacity: 0.3;
	/* animation: fire_boom_s 2s ease infinte;
	-webkit-animation: fire_boom_s 2s ease infinite; */
}
.fire-item.item3 {
	top: -20px;
	left: 200px;
	animation: fire_boom_s 1.5s ease infinte;
	-webkit-animation: fire_boom_s 1.5s ease infinite;
}
.fire-item.item4 {
	width: 40px;
	height: 40px;
	right: 30px;
	top: 90px;
	opacity: 0.5;
	animation: fire_boom_s 2.5s ease infinte;
	-webkit-animation: fire_boom_s 2.5s ease infinite;
}
.fire-item.item5 {
	width: 20px;
	height: 20px;
	left: 40px;
	top: 100px;
	opacity: 0.5;
	animation: fire_boom_s 3s ease infinte;
	-webkit-animation: fire_boom_s 3s ease infinite;
}
.theme-bg .text-box {
	width: 330px;
	height: 80px;
	margin: 30px auto 0 auto;
	background: url(https://s1.wandougongzhu.cn/s/46/16_1d7c08.png) no-repeat;
	background-size: 100% auto;
} 
.tips {
	margin-top: 90px;
	font-size: 16px;
	color: rgb(237, 61, 98);
	text-align: center;
	font-weight: bold;
}
.reel-box {
	width: 100%;
	height: 453px;
	margin-top: -28px;
	background: url(https://s5.wandougongzhu.cn/s/16/bg_ae5f7d.png) no-repeat;
	background-size: cover;
	position: relative;
}
.reel-box .flower-box {
	width: 100%;
	height: 360px;
}
.reel-box .flower-box .flower-item {
	position: absolute;
	overflow: visible;
}
.flower-item .tag{
	position: relative;
	width: 23px;
	padding: 10px 2px;
	font-size: 10px;
	font-weight: bold;
	line-height: 11px;
	color: #000;
	box-sizing: border-box;
	background: url(https://s1.wandougongzhu.cn/s/ec/2x_9bfe98.png) no-repeat;
	background-size: 100% 100%;
	background-position: center;
	z-index: 1;
	display: flex;
	align-items: center;
	justify-items: center;
}
.flower-item .tag.gray {
	background: url(https://s4.wandougongzhu.cn/s/20/_gray_cd255c.png) no-repeat;
	background-size: 100% 100%;
}
.flower-item .num-box {
	position: absolute;
	right: -8px;
	bottom: -6px;
}
.flower-item .fire-ani-box {
	width: 100%;
	height: 100%;
	position: absolute;
	left: 0;
	top: 0;
}
.fire-ani-box .firecracker {
	width: 16px;
	height: 33px;
	position: absolute;
	background: url(https://s5.wandougongzhu.cn/s/bd/_d9b697.png) no-repeat;
	background-size: 100% 100%;
	z-index: 1;
}
.firecracker .ani {
	left: 6px;
	bottom: 30px;
	position: absolute;
	width: 2px;
	height: 6px;
	border-radius: 70%;
	background-image: linear-gradient(to bottom, rgb(213, 34, 35),rgba(255,255,255,0.5));
	background-size: cover;
	/* forwards */
	animation: fire_rise 2s forwards cubic-bezier(.08,.47,.38,.87);
}
.firecracker .boom {
	position: absolute;
	bottom: 70px;
	left: -26px;
	width: 60px;
	height: 60px;
	border-radius: 50%;
	transform: scale(0.5);
	opacity: 0;
	background: url(https://s.wandougongzhu.cn/s/49/42x_154024.png) no-repeat;
	background-size: cover;
	animation: fire_boom_s 2s forwards ease-in-out;
	animation-delay: 2.5s;
}
.flower-item-dyh {
	left: 246px;
	top: 59px;
	width: 105px;
	height: 90px;
	background: url(https://s1.wandougongzhu.cn/s/1b/dyh_map_328482.png) no-repeat;
	background-size: cover;
	background-position: center;
}
.flower-item-dyh.gray {
	background: url(https://s3.wandougongzhu.cn/s/9c/_gray_ab60a2.png) no-repeat;
	background-size: cover;
	background-position: center;
}
.flower-item-dq {
	left: 169px;
	top: 145px;
	width: 101px;
	height: 92px;
	background: url(https://s5.wandougongzhu.cn/s/63/dq_map_440614.png) no-repeat;
	background-size: cover;
	background-position: center;
}
.flower-item-dq.gray {
	background: url(https://s4.wandougongzhu.cn/s/9d/dq_map_g_5b5429.png) no-repeat;
	background-size: cover;
	background-position: center;
}
.flower-item-tf {
	left: 147px;
	top: 187px;
	width: 90px;
	height: 90px;
	background: url(https://s5.wandougongzhu.cn/s/8d/tf_map_489ec1.png) no-repeat;
	background-size: cover;
	background-position: center;
}
.flower-item-tf.gray {
	background: url(https://s5.wandougongzhu.cn/s/53/tf_map_g_81d879.png) no-repeat;
	background-size: cover;
	background-position: center;
}
.flower-item-db {
	left: 56px;
	top: 227px;
	width: 104px;
	height: 60.5px;
	background: url(https://s.wandougongzhu.cn/s/e3/db_map_065caa.png) no-repeat;
	background-size: cover;
	background-position: center;
}
.flower-item-db.gray {
	background: url(https://s4.wandougongzhu.cn/s/00/db_map_g_262ac2.png) no-repeat;
	background-size: cover;
	background-position: center;
}
.flower-item-zhc {
	left: 24px;
	top: 246px;
	width: 100.5px;
	height: 61px;
	background: url(https://s4.wandougongzhu.cn/s/d0/zhc_map_128e65.png) no-repeat;
	background-size: cover;
	background-position: center;
}
.flower-item-zhc.gray {
	background: url(https://s4.wandougongzhu.cn/s/2b/zhc_map_g_f9ac74.png) no-repeat;
	background-size: cover;
	background-position: center;
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
	width: 100%;
	height: 260px;
}
.universal-flower .flower-item {
	position: absolute;
	overflow: visible;
}
.universal-flower .flower-item-dyh {
	left: 195px;
	top: 80px;
	width: 78px;
	height: 68px;
}
.universal-flower .flower-item-dq {
	left: 128px;
	top: 145px;
	width: 83px;
	height: 74px;
}
.universal-flower .flower-item-tf {
	left: 113px;
	top: 178px;
	width: 70px;
	height: 73px;
}
.universal-flower .flower-item-db {
	left: 45px;
	top: 210px;
	width: 81px;
	height: 46px;
}
.universal-flower .flower-item-zhc {
	left: 19px;
	top: 223px;
	width: 80px;
	height: 48px;
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
.mix-btn {
	position: absolute;
	right: 22px;
	bottom: 36px;
	display: block;
	width: 60px;
	height: 60px;
	padding: 0;
	color: rgba(255, 255, 255, 0.302);
	font-size: 16px;
	line-height: 18px;
	background: none;
	color: rgba(255,255,255,1);
	background: url('https://s2.wandougongzhu.cn/s/4c/-2x_81cff2.png') no-repeat;
	background-size: cover;
	overflow: hidden;
	border-radius: 50%;
}
.wave {  
	position: absolute;
	top: 0;
	width: 60px;  
	height: 60px;  
	background: url('https://s2.wandougongzhu.cn/s/4c/-2x_81cff2.png') no-repeat;
	background-size: cover; 
	border-radius: 50%; 
	overflow: hidden; 
}
.wave-pos {
	width: 60px;
	height: 60px;
	background: transparent;
	position: relative;
	z-index: 2;
	overflow: hidden;
}
.wave-pos-before,  
.wave-pos-after {
	display: block; 
	position: relative;
	width: 80px;  
	height: 80px;  
	top: 0;  
	left: 50%;  
	background-color: rgba(0, 0, 0, .2);
	border-radius: 34%;  
	transform: translate(-50%, -18px) rotate(0);  
	animation: rotate 7s linear infinite;  
	z-index: 1;  
}  
.wave-pos-after {  
	top: -80px;
	border-radius: 67%;  
	background-color: rgba(0, 0, 0, .5);  
	transform: translate(-50%, -18px) rotate(0);  
	animation: rotate 11s linear -5s infinite;
}
@keyframes rotate {  
	50% {  
		transform: translate(-50%, -18px) rotate(180deg);  
	} 100% {  
		transform: translate(-50%, -18px) rotate(360deg);  
	}  
} 
.mix-btn-text {
	position: absolute;
	width: 60px;
	height: 60px;
	padding: 12px 10px;
	box-sizing: border-box;
	color: #fff;
	z-index: 2;
}
.flower-box .bottom {
	display: flex;
	justify-content: center;
}
.rest-count {
	color: rgb(0,0,0);
	font-size: 12px;
	text-align: center;
	margin-top: 30px;
	position: relative;
}
.lottery-btn {
	font-size: 18px;
	font-weight: bold;
	display: block;
	width: 150px;
	height: 38px;
	line-height: 38px;
	color: #fff;
	text-align: center;
	background: url('https://s2.wandougongzhu.cn/s/09/-_f9c638.png') no-repeat;
	background-size: 100% 100%;
	margin: 5px auto;
	animation: breath 2s ease infinte;
	-webkit-animation: breath 2s ease infinite;
}
.lottery-btn.wait-res {
	background: url('https://s3.wandougongzhu.cn/s/3b/-_gray_673f6c.png') no-repeat;
	background-size: 100% 100%;
}
.task-title,.rule-title {
	position: relative;
	width: 345px;
	height: 50px;
	line-height: 50px;
	margin: 10px auto;
	font-size: 18px;
	font-weight: bold;
	color: rgba(255, 235, 206, 1);
	background: url(https://s1.wandougongzhu.cn/s/65/122x_130aa0.png) no-repeat;
	background-size: contain;
	background-position: center;
	display: flex;
	flex-direction: column;
	align-content: center;
}
.rule-title {
	background: none;
}
.brand-title-tips {
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
	font-weight: bold;
	line-height: 60px;
	color: #191919;
	margin: 10px auto;
	padding-left: 10px;
	box-sizing: border-box;
	display: flex;
	background: url('https://s5.wandougongzhu.cn/s/22/1_2ddd54.png') no-repeat;
	background-size: 100% 100%;
}
.suc-box {
	line-height: 30px;
	display: flex;
}
.suc-box-right {
	display: flex;
	align-items: center;
	font-size: 14px;
	text-align: left;
}
.suc-box-right span {
	color: #d42223;
}
.task-item-img {
	position: absolute;
	right: 110px;
	margin: 20px 0;
}
.task-item-img img {
	width: 50px;
	height: 54px;
}
.task-item-btn {
	position: absolute;
	right: 10px;
	margin: 20px;
	font-size: 14px;
	line-height: 24px;
	text-align: center;
	padding: 0;
	display: block;
	width: 62px;
	height: 24px;
	background: rgb(248, 233, 209);
	color: rgb(73, 15, 0);
	border-radius: 0;
}
.task-item-btn.done {
  color: rgb(237, 218, 180);
	border: 1.5px solid rgb(237, 218, 180);
	transform: rotate(30deg);
	background: transparent;
	transform: rotate(-10deg);
	margin: 18px 20px;
	box-sizing: border-box;
}
.task-item-btn.receive {
	color: rgb(73, 15, 0);
	background: url('https://s5.wandougongzhu.cn/s/f8/ing_fe1225.png') no-repeat;
	background-size: 100% 100%;
}
.task-item-btn button {
	display: block;
	font-size: 14px;
	width: 62px;
	height: 24px;
	line-height: 24px;
	padding: 0;
	border: none;
	background: none;
}
#mask,.compose-box {
	text-align: center;
	display: flex;
	justify-content: center;
	align-items: center;
	z-index: 2;
}
.compose-ani {
	opacity: 0;  
	position: absolute;
	width: 220px;
	height: 220px;
	left: 10px;
	bottom: 250px;
	z-index: 1;
	background: url('https://s4.wandougongzhu.cn/s/34/1_ae06eb.png') no-repeat;
	background-size: cover;
	-webkit-animation: fire_boom 2.5s forwards cubic-bezier(.01,.43,.34,.91);
	animation: fire_boom 2.5s forwards cubic-bezier(.01,.43,.34,.91);
	animation-delay: 1s;
}
.compose-ani-before {
	opacity: 0;  
	position: absolute;
	left: 100px;
	width: 28px;
	height: 100px;
	background: url('https://s.wandougongzhu.cn/s/fb/4_b2c3de.png') no-repeat;
	background-size: cover;
	background-position: center;
	bottom: 265px;
	animation: fire_boom_up 1s forwards cubic-bezier(.07,.72,.56,1);
}
.compose-ani-2 {
	opacity: 0;  
	position: absolute;
	width: 190px;
	height: 190px;
	left: 190px;
	bottom: 190px;
	z-index: 2;
	background: url('https://s5.wandougongzhu.cn/s/a5/2_8ef911.png') no-repeat;
	background-size: cover;
	-webkit-animation: fire_boom 2.5s forwards cubic-bezier(.01,.43,.34,.91);
	animation: fire_boom 2.5s forwards cubic-bezier(.01,.43,.34,.91);
	animation-delay: 1s;
}
.compose-ani2-before {
	opacity: 0;  
	position: absolute;
	left: 270px;
	width: 28px;
	height: 100px;
	background: url('https://s1.wandougongzhu.cn/s/be/1_236cef.png') no-repeat;
	background-size: cover;
	background-position: center;
	bottom: 210px;
	animation: fire_boom_up 1s forwards cubic-bezier(.07,.72,.56,1);
}
.compose-ani-3 {
	opacity: 0;  
	position: absolute;
	width: 100px;
	height: 100px;
	left: 288px;
	bottom: 405px;
	z-index: 1;
	background: url('https://s2.wandougongzhu.cn/s/64/3_fe2423.png') no-repeat;
	background-size: cover;
	-webkit-animation: fire_boom 2.3s forwards cubic-bezier(.01,.43,.34,.91);
	animation: fire_boom 2.3s forwards cubic-bezier(.01,.43,.34,.91);
	animation-delay: 1.2s;
}
.compose-ani3-before {
	opacity: 0; 
	position: absolute;
	left: 85px;
	width: 22px;
	height: 75px;
	background: url('https://s.wandougongzhu.cn/s/bf/3_7bb5d1.png') no-repeat;
	background-size: cover;
	background-position: center;
	bottom: 433px;
	animation: fire_boom_up 1s forwards cubic-bezier(.07,.72,.56,1);
}
.compose-ani-4 {
	opacity: 0; 
	position: absolute;
	width: 170px;
	height: 170px;
	left: 10px;
	bottom: 405px;
	z-index: 1;
	background: url('https://s2.wandougongzhu.cn/s/02/4_9f75e9.png') no-repeat;
	background-size: cover;
	-webkit-animation: fire_boom 2.5s forwards cubic-bezier(.01,.43,.34,.91);
	animation: fire_boom 2.5s forwards cubic-bezier(.01,.43,.34,.91);
	animation-delay: 1s;
}
.compose-ani4-before {
	opacity: 0; 
	position: absolute;
	left: 328px;
	width: 28px;
	height: 100px;
	background: url('https://s.wandougongzhu.cn/s/fb/4_b2c3de.png') no-repeat;
	background-size: cover;
	background-position: center;
	bottom: 380px;
	animation: fire_boom_up 1s forwards cubic-bezier(.07,.72,.56,1);
	animation-delay: .2s;
}
.compose-ani-5 {
	opacity: 0; 
	position: absolute;
	width: 290px;
	height: 290px;
	left: 70px;
	bottom: 310px;
	z-index: 2;
	background: url('https://s3.wandougongzhu.cn/s/10/5_66436a.png') no-repeat;
	background-size: cover;
	-webkit-animation: fire_boom 2s forwards cubic-bezier(.01,.43,.34,.91);
	animation: fire_boom 2s forwards cubic-bezier(.01,.43,.34,.91);
	animation-delay: 1.5s;
}
.compose-ani5-before {
	opacity: 0; 
	position: absolute;
	left: 208px;
	width: 28px;
	height: 100px;
	background: url('https://s.wandougongzhu.cn/s/32/2_6dc082.png') no-repeat;
	background-size: cover;
	background-position: center;
	bottom: 360px;
	animation: fire_boom_up 1s forwards cubic-bezier(.07,.72,.56,1);
	animation-delay: 0.5s;
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
@-webkit-keyframes breath {
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
@keyframes fire_rise{
	0%{  
		bottom: 25px;
	}
	90% {
		opacity: 1;
		bottom: 80px;
	}
	100%{
		bottom: 80px;
		opacity: 0;
	}  
} 
@-webkit-keyframes fire_rise{
	0%{  
		bottom: 25px;
	}
	90% {
		opacity: 1;
		bottom: 80px;
	}
	100%{
		bottom: 80px;
		opacity: 0;
	}  
}

@keyframes fire_boom_s {
	0%{
		transform: scale(0.5); 
		opacity:1;
	}
	80%{ 
		opacity: 0.2;
		transform: scale(1);
	}
	100%{ 
		opacity: 0; 
		transform:scale(1);
	}
}
@-webkit-keyframes fire_boom_s {
	0%{
		transform: scale(0.5); 
		opacity:1;
	}
	80%{ 
		opacity: 0.2;
		transform: scale(1);
	}
	100%{ 
		opacity: 0; 
		transform:scale(1);
	}
}
@keyframes fire_boom {
	0%{
		transform: scale(0.03) translateY(400px); 
		opacity: 1;
	}
	10% {
		transform: scale(0.03) translateY(20px); 
		opacity: 1;
	}
	90%{ 
		opacity: 1;
		transform:scale(1) translateY(0);
	}
	100%{ 
		opacity: 0;
		transform:scale(1) translateY(0);
	}
}
@-webkit-keyframes fire_boom {
	0%{
		transform: scale(0.03) translateY(400px); 
		opacity: 1;
	}
	10% {
		transform: scale(0.03) translateY(20px); 
		opacity: 1;
	}
	90%{ 
		opacity: 1;
		transform:scale(1) translateY(0);
	}
	100%{ 
		opacity: 0;
		transform:scale(1) translateY(0);
	}
}
@keyframes fire_boom_up {
	0% {
		opacity: 0.5;
		bottom: 0;
	}
	90% {
		opacity: 1;
	}
	100% {
		opacity: 0;
	}
}
.ani-delay {
	animation-delay: 0.5s;
}
.brand-box {
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
}
.brand-box-content {
	width: 352px;
	height: 250px;
	padding: 20px 0;
	background: url(https://s4.wandougongzhu.cn/s/a2/alert_s_f4973c.png) no-repeat;
	background-size: 100% 100%;
	margin: 0 auto;
	color: rgb(25, 25, 25);
  font-size: 16px;
}
/* https://s4.wandougongzhu.cn/s/a2/alert_s_f4973c.png */
.brand-box-top{
	width: 345px;
	height: 220px;
	overflow: hidden;
	margin: 0 auto;
	display: flex;
	flex-direction: column;
	justify-content: center;
	flex-wrap: wrap;
}
.brand-box-top-item,.brand-box-my{
	position: relative;
	width: 310px;
	height: 40px;
	margin: 0 auto;
	display: flex;
	align-items: center;
	justify-content: space-between;
}
.brand-box-my {
	width: 310px;
	margin: 0 auto;
	height: 40px;
	border-bottom: 0.5px solid rgb(196, 163, 97);
}
.brand-box-top-item .img-box {
	font-size: 12px;
	display: flex;
	flex-direction: row;
	justify-content: center;
	align-content: center;
}
.brand-box-top-item .img-box img{
	position: relative;
	width: 25px;
	height: 25px;
	margin: 0 5px;
	border-radius: 50%;
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
	width: 25px;
	height: 25px;
	margin: auto 10px;
	font-size: 10px;
	color: #fff;
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
}
.brand-box-top-item .rank img {
	width: 25px;
	height: 25px;
	margin: 0;
}
.brand-box-top-item .rank .num {
	color: #ea4141;
	font-size: 10px;
}
.brand-box-top-item .rank .last {
	width: 20px;
	height: 20px;
	border-radius: 50%;
	text-align: center;
	font-size: 10px;
	line-height: 20px;
	background: rgb(0, 0, 0);
}
.brand-box-top-item .flower-box {
	flex: 1;
	text-align: right;
	font-size: 10px;
}
.brand-box-top-item .flower-box .flower {
	color: #ea4141;
}
.brand-box-top-item .rank .desc,.brand-box-top-item .flower-box .time {
  color: rgb(158, 158, 158);
  font-size: 8px;
	white-space: nowrap;
}

</style>

 