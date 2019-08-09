<template>
	<div class="container">
		<div class="title">请选择要赠送的花火</div>
		<swiper class="swiper-box" next-margin="35px" previous-margin="35px" @change="swiperChange">
			<swiper-item v-for="item in sakuraList" :key="item.index">
				<div class="get-alert-box" >
					<div class="sakura-text">
						<div class="name">{{item.sakura_name}}</div>
						<div class="ihave-sakura">拥有<span>{{item.sakura_num}}</span>瓣</div>
					</div>
					<img v-if="item.sakura_key == 'sakura_a'" class="mysakura" src="https://s4.wandougongzhu.cn/s/3a/zhc_8eeb51.jpg">
					<img v-if="item.sakura_key == 'sakura_b'" class="mysakura" src="https://s1.wandougongzhu.cn/s/92/tf_61b463.jpg">
					<img v-if="item.sakura_key == 'sakura_c'" class="mysakura" src="https://s3.wandougongzhu.cn/s/9f/dyh_984083.jpg">
					<img v-if="item.sakura_key == 'sakura_d'" class="mysakura" src="https://s3.wandougongzhu.cn/s/72/dq_196ee4.jpg">
					<img v-if="item.sakura_key == 'sakura_e'" class="mysakura" src="https://s3.wandougongzhu.cn/s/b9/db_d1cdb7.jpg">
					<div class="mysakura-tips">
						<p>多余的樱花瓣可以赠送给好友哦</p>
						<p>每天首次赠送可获得1次抽樱花瓣的机会</p>
					</div>
				</div>
			</swiper-item>
		</swiper>
		<form :report-submit="form_id" @submit="gather" >
			<button class="mysakura-btn" form-type="submit" @click="sendToFriendShow()"> 
				送给好友
			</button>
		</form>
		<div id="mask" v-if="maskShow">
			<!-- 分享成功告诉好友 -->
			<div class="get-alert-box suc-alert-box" v-if="showAlert == 'sendToFriend'">
				<div class="colse" @click="closeAlert()"></div>
				<div class="mysakura-text">
					<div class="name">樱花瓣已扣除，快去分享给好友吧！</div>
				</div>
				<form :report-submit="form_id" @submit="gather" >
					<button open-type="share" class="mysakura-btn">
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
			sakuraList: [
				{
					'sakura_num': 1,
					'sakura_name': '筑后川花火大会',
					'sakura_key': 'sakura_a',
					'share_img': 'https://s4.wandougongzhu.cn/s/3a/zhc_8eeb51.jpg'
				},{
					'sakura_num': 2,
					'sakura_name': '土浦花火大会',
					'sakura_key': 'sakura_b',
					'share_img': 'https://s1.wandougongzhu.cn/s/92/tf_61b463.jpg'
				},{
					'sakura_num': 3,
					'sakura_name': '洞爷湖花火大会',
					'sakura_key': 'sakura_c',
					'share_img': 'https://s3.wandougongzhu.cn/s/9f/dyh_984083.jpg'
				},{
					'sakura_num': 4,
					'sakura_name': '大曲花火大会',
					'sakura_key': 'sakura_d',
					'share_img': 'https://s3.wandougongzhu.cn/s/72/dq_196ee4.jpg'
				},{
					'sakura_num': 5,
					'sakura_name': '大阪天神祭',
					'sakura_key': 'sakura_e',
					'share_img': 'https://s3.wandougongzhu.cn/s/b9/db_d1cdb7.jpg'
				},
			], //已有樱花数量
			shareImgBtn: '', //分享花瓣给好友图 sakura_a
			shareImg: 'https://s4.wandougongzhu.cn/s/e4/__1_17ae88.jpg', //分享图
			sakuraDetailRotate: 0, //旋转角度
			shareSakuraKey: '', //分享的樱花key
			shareSakuraName: '', //分享的樱花name
			sakura_id: '',
			maskShow: false,
			showAlert: '',
		};
	},
	onLoad(option) {
		console.log(option);
		let ch = 'sakura_mp_2019';
		wx.hideShareMenu();
		wx.setStorage({ key: 'ch', data: ch });
		WMP.globalData.ch = ch;

		wx.hideShareMenu();
		this.userInfo = WMP.globalData.userInfo;
		this.user_id = this.userInfo.user_id;
		this.getUserActInfo();
	},
	// created() {
	// 	this.userInfo = WMP.globalData.userInfo;
	// 	this.user_id = this.userInfo.user_id;
	// 	this.getUserActInfo();
	// },
	onShareAppMessage (res) {
		console.log(res)
		let self = this;

		if (res.from == 'button') {
			wx.nextTick(function () {
				Net.tick({
					type: 'sakura_share_flower'
				});
				self.closeAlert();
				self.showAlert = '';
				self.maskShow = false;
				self.getUserActInfo();
			});
			return {
				title: '送你一朵'+this.shareSakuraName+'，快来和我平分100万现金！',
				path: '/pages/fireworks/main?sakura_key=' + this.shareSakuraKey +'&user_id=' + this.user_id + "&sakura_id=" + this.sakura_id,
				imageUrl: this.shareImgBtn,
				success: function (res) {
					wx.showToast({
						title: '分享成功',
						icon: 'success',
						duration: 2000
					});
					wx.navigateTo({
						url: '/pages/fireworks/main?user_id=' + this.user_id
					});
				},
				fail: function () {
					wx.showToast({
						title: '取消分享',
						icon: 'none',
						duration: 2000
					});
				}
			}
		} else {
			let shareImg = this.shareImg;
			return {
				title: '100万现金等你来分！距离分钱仅剩'+this.restDay+'天！',
				path: '/pages/fireworks/main?user_id=' + this.user_id,
				imageUrl: shareImg,
				success: function (res) {
					wx.showToast({
						title: '分享成功',
						icon: 'success',
						duration: 2000
					});
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
		}
		
	},
	methods: {
		gather(e) {
			console.log(e);
			Net.gatherMsgId({
				scene_id: 7,
				scene_val: 'sakura',
				form_id: e.mp.detail.formId,
			});
		},
		sendToFriendShow() {
			console.log('sendtof');
			Net.get('Sakura.userGiftSakura', {
				data: {
					user_id: this.user_id,
					sakura_key: this.shareSakuraKey
				}
			}).then(res=>{
				if(res.errno=='0') {
					this.sakura_id = res.data.sakura_id;
					console.log("sakura_id=" + this.sakura_id);
					this.maskShow = true;
					this.showAlert = 'sendToFriend';
				} else {
					wx.showModal({title:'提示', content: res.errmsg});
				}
			});
		},
		swiperChange(res){
			let current = res.target.current;
			this.shareSakuraKey = this.sakuraList[current].sakura_key || this.sakuraList[0].sakura_key;
			this.shareSakuraName = this.sakuraList[current].sakura_name || this.sakuraList[0].sakura_name;
			this.shareImgBtn = this.sakuraList[current].share_img || this.sakuraList[0].share_img;
		},
		getUserActInfo() {
			Net.get('Sakura.getUserActivityInfoByUserId', {
				user_id: this.user_id
			}).then(res=>{
				let sakuraitem = res.data.info;
				console.log(`sakuraitem=` + sakuraitem)
				let list = [];
				if (sakuraitem.sakura_a > 0) {
					list.push({
						'sakura_num': sakuraitem.sakura_a,
						'sakura_name': '筑后川花火大会',
						'sakura_key': 'sakura_a',
						'share_img': 'https://s4.wandougongzhu.cn/s/3a/zhc_8eeb51.jpg'
					});
				}
				if (sakuraitem.sakura_b > 0) {
					list.push({
						'sakura_num': sakuraitem.sakura_b,
						'sakura_name': '土浦花火大会',
						'sakura_key': 'sakura_b',
						'share_img': 'https://s1.wandougongzhu.cn/s/92/tf_61b463.jpg'
					});
				}
				if (sakuraitem.sakura_c > 0) {
					list.push({
						'sakura_num': sakuraitem.sakura_c,
						'sakura_name': '洞爷湖花火大会',
						'sakura_key': 'sakura_c',
						'share_img': 'https://s3.wandougongzhu.cn/s/9f/dyh_984083.jpg'
					});
				}
				if (sakuraitem.sakura_d > 0) {
					list.push({
						'sakura_num': sakuraitem.sakura_d,
						'sakura_name': '大曲花火大会',
						'sakura_key': 'sakura_d',
						'share_img': 'https://s3.wandougongzhu.cn/s/72/dq_196ee4.jpg'
					});
				}
				if (sakuraitem.sakura_e > 0) {
					list.push({
						'sakura_num': sakuraitem.sakura_e,
						'sakura_name': '大阪天神祭',
						'sakura_key': 'sakura_e',
						'share_img': 'https://s3.wandougongzhu.cn/s/b9/db_d1cdb7.jpg'
					});
				}
				this.sakuraList = list;
				this.shareImgBtn = this.sakuraList[0].share_img;
				this.shareSakuraKey = this.sakuraList[0].sakura_key;
				this.shareSakuraName = this.sakuraList[0].sakura_name;
			});
		},
		closeAlert (param) {
			param = false;
			this.maskShow = false;
		}
	},

};
</script>

<style scoped>
button::after{
	display: none;
}
#mask {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	background: rgba(0,0,0,.7);
	text-align: center;
	display: flex;
	justify-content: center;
	align-items: center;
}
.get-alert-box,.compose-box {
	position: absolute;
	left: 50%;
	top: 50%;
	transform: translate(-50%,-50%);
	width: 300px;
	height: 345px;
	font-size: 14px;
	text-align: center;
	background: url('https://s3.wandougongzhu.cn/s/cc/alert_7c4ab3.png') no-repeat;
	background-size: 100% 100%;
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
.container {
	position: absolute;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	text-align: center;
	background: url('https://s1.wandougongzhu.cn/s/5c/_a225a7.jpg') no-repeat;
	background-size: 100% 100%;
	background-color: #f3f2f1;
	padding: 0;
	margin: 0;
}
.title {
	font-size: 22px;
  color: #fff;
	text-align: center;
	font-weight: bold;
	margin-top: 80px;
}
.swiper-box {
	position: absolute;
	top: 50%;
	transform: translate(0,-50%);
	width: 375px;
	height: 345px;
	/* padding: 0 95px; */
	overflow: hidden;
}
.mysakura-text {
	margin-top: 28px;
}
.sakura-text .name {
	margin-top: 20px;
	font-size: 20px;
	line-height: 22px;
	font-weight: bold;
  color: rgb(213, 34, 35);
}
.mysakura{
	width: 260px;
	height: 177px;
	position: relative;
	margin: 15px auto;
}
.mysakura-tips {
	color: rgb(67, 67, 67);
	bottom: 60px;
	font-size: 12px;
	line-height: 20px;
	text-align: center;
}
.ihave-sakura {
	color: #191919;
	font-size: 14px;
	margin-top: 5px;
	font-weight: bold;
}
.ihave-sakura span {
	color: rgb(255, 29, 95);
	margin: 0 2px;
}
.mysakura-btn {
	position: absolute;
	left: 50%;
	transform: translate(-50%,0);
	bottom: 50px;
	width: 115px;
	height: 38px;
	line-height: 38px;
	font-size: 14px;
	color: #fff;
	border: none;
	background: url('https://s5.wandougongzhu.cn/s/09/_ad9e3d.png') no-repeat;
	background-size: 100% 100%;
	margin: 0 auto;
}

.tips {
	font-size: 16px;
	color: rgb(87, 94, 137);
	display: flex;
	text-align: center;
}
</style>
