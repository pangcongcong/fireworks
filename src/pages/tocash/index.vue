<template>
	<div class="container">
		<div class="tips">
			<div>我合成的花火</div>
			<div class="my-sakura-box" v-if="sakura_H_num > 0">
				<div class="my-sakura">X{{sakura_H_num || 0}}</div>
			</div>
			<div class="none-tips" v-if="sakura_H_num == '0'">无可兑换的花火</div>
			<div class="min-tips" v-if="user_price == '0' && toCashNum < min_exchange_price">微信限制提现金额不得小于0.3元，建议兑换豌豆积分</div>
		</div>
		<div class="duihuan-box">
			<div class="cash-box">
				<img class="icon" src="https://s5.wandougongzhu.cn/s/ca/xianjin_82b0bb.png" alt="">
				<div class="cash-content">
					<div class="tips2">
						<span>{{toCashNum || 0}}</span>元
						<div class="mini-tip">24小时内存入微信零钱</div>
					</div>
					
					<div v-if="user_price != '' && user_price != '0'" class="to-cash-btn to-cash-btn-disable">
						<text v-if="pay_status == '2'">已兑换</text>
						<text v-else>已失效</text>
					</div>
					<form v-if="user_price == '0' || user_price == ''" :report-submit="form_id" @submit="gather" >
						<button class="to-cash-btn" form-type="submit" @click="showChangeCash()">
							兑换现金
						</button>
					</form>
				</div>
			</div>
			<div class="score-box">
				<img class="icon" src="https://s3.wandougongzhu.cn/s/ad/jifen_964890.png" alt="">
				<div class="cash-rate">{{score_rate}}倍</div>
				<div class="score-content">
					<div class="tips2">
						<div>价值<span>{{scoreToCash}}</span>元({{toScoreNum}})积分</div>
						<div class="mini-tip">下单可直接抵现</div>
					</div>
					<div v-if="user_price != '' && user_price != '0'" class="to-cash-btn to-cash-btn-disable">
						<text v-if="pay_status == '3'">已兑换</text>
						<text v-else>已失效</text>
					</div>
					<form v-if="user_price == '0' || user_price == ''" :report-submit="form_id" @submit="gather" >
						<button class="to-score-btn" form-type="submit" @click="toScore()">
							兑换积分
						</button>
					</form>
				</div>
			</div>
		</div>
		<div id="mask" v-if="maskShow">
			<div class="to-alert-box" v-show="showAlert == 'changescore'">
				<div class="colse" @click="closeAlert()"></div>
				<div class="changecash-title">积分兑换提醒</div>
				<div class="mysakura-tips">
					<p>即将为您兑换豌豆公主<span>{{toScoreNum}}</span>积分，</p>
					<p>可抵现<span>{{scoreToCash}}</span>元，下单时可抵现。</p>
				</div>
				<div class="btn-box">
					<div class="mysakura-btn dis-btn" @click="closeAlert()">
						取消
					</div>
					<div class="mysakura-btn" @click="showChangeScore()">
						去兑换
					</div>
				</div>
			</div>
			<div class="to-alert-box alert-new-box changecash"  v-if="showAlert == 'changescash'">
				<div class="colse" @click="closeAlert()"></div>
				<div class="changecash-title">兑换现金提醒</div>
				<div class="mysakura-tips">
					<p>受微信规则限制，兑换的现金需通过公众号发到您的手中。请在微信搜索公众号「豌豆公主服务号」并关注，再点击按钮兑换现金。</p>
				</div>
				<div class="btn-box">
					<div class="mysakura-btn" @click="showChangeCash()">
						我知道了
					</div>
				</div>
			</div>
		</div>
		<div id="suc" v-if="sucResShow">
			<div class="suc-title">恭喜您，<span v-if="type == '0'">积分</span> <span v-if="type == '1'">现金</span>兑换成功！</div>
			<div class="suc-tips" v-if="type == '0'">积分已经放入豌豆公主账号<span>{{phone}}</span></div>
			<div class="suc-tips" v-if="type == '1'">现金24小时内会存入您的微信钱包</div>
			<div class="suc-res" v-if="type == '0'">{{toScoreNum}}<span>积分</span></div>
			<div class="suc-res" v-if="type == '1'">{{toCashNum}}<span>现金</span></div>
			<div v-if="type == '1' && toCashNum < 1">
				<div class="suc-tips">{{toCashTip}}</div>
				<!-- <img class="to-cash-tip" src="https://s4.wandougongzhu.cn/s/f3/613_360bb0.png" alt=""> -->
			</div>
			<div @click="toAd(ad_info.page_id)" >
				<img v-bind:src="ad_info.ad_img" alt="" class="suc-banner">
			</div>
			<form :report-submit="form_id" @submit="gather" >
				<button form-type="submit" class="suc-btn" @click="toIndex">
					去逛逛
				</button>
			</form>
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
			toCashNum: 0,
			toScoreNum: 0,
			maskShow: false,
			sucResShow: false,
			scoreToCash: 0,
			toCashTip: '',
			type: null,
			phone: '',
			realMoney: '',
			sakura_H_num: '0',
			ad_info: {}, //广告
			score_rate:'', //
			user_price: '', //兑换过了
			min_exchange_price: '', //最小金额
			pay_status: '0',//
			logCommonParam: {
				ns: '828_huahuodahui_mp',
				w: '',
				open_id: '',
				devtype: 'mp',
				ch: ch,
			},
			showAlert: ''//兑换现金 changescash or 积分 changescore
		};
	},
	onLoad(option) {
		console.log(option);
		wx.hideShareMenu();
		wx.setStorage({ key: 'ch', data: ch });
		WMP.globalData.ch = ch;
		this.logCommonParam.open_id = WMP.getOpenid() || null;
		// getInfo().then(()=> {
			WMP.checkAuthPromise(this.$root.$mp.page).then(res=> {
				this.userInfo = WMP.globalData.userInfo;
				this.user_id = this.userInfo.user_id;
				this.getUserActInfo();
			})
		// })
	},
	methods: {
		toAd(page_id) {
			Net.newLog(
				{
					mt: 'huahuodahui_gotoad',
				},
				this.logCommonParam,
			);
			if (page_id && page_id != '0') {
				wx.navigateTo({ url:  `/page/page/index?page_id=${page_id}`});
			} else {
				wx.switchTab({ url: '/page/index/index'});
			}
		},
		gather(e) {
			console.log(e);
			Net.gatherMsgId({
				scene_id: 7,
				scene_val: 'huahuodahui',
				form_id: e.mp.detail.formId,
			});
		},
		bindViewTap() {
			const url = '../logs/logs';
			wx.navigateTo({ url });
		},
		toScore() {
			if (this.toScoreNum > 0) {
				this.showAlert = 'changescore';
				this.maskShow = true;
			} else {
				wx.showToast({
					title: '无可兑换积分',
					icon: 'none',
					duration: 2000,
				})
			}
		},
		toIndex() {
			wx.switchTab({
				url: '/page/index/index'
			});
		},
		getUserActInfo() {
			this.userInfo = WMP.globalData.userInfo;
			this.user_id = this.userInfo.user_id;
			Net.get('Sakura.getUserActivityInfoByUserId', {
				user_id: this.user_id
			}).then(res=>{
				if (res.errno == '0') {
					let infoList = res.data.info;
					
					this.toCashNum = res.data.user_exchange_price;
					this.toScoreNum = res.data.user_exchange_score;
					this.scoreToCash = res.data.score_to_cash;
					this.sakura_H_num = parseInt(infoList.sakura_h);
					this.ad_info = res.data.ad_info;
					this.score_rate = res.data.score_rate;
					this.user_price = infoList.price;
					this.min_exchange_price = res.data.min_exchange_price;
					this.pay_status = infoList.pay_status;
					this.phone = infoList.phone;
					this.toCashTip = res.data.to_cash_tips;
					if (this.pay_status != 0) {
						this.sucResShow = true;
						this.type = this.pay_status == '2' ? '1':'0';
					}
				} else {
					wx.showToast({
						title: res.errmsg,
						icon: 'none',
						duration: 2000,
					});
				}
			});
		},
		showChangeScore() {
			Net.get('Sakura.userExchange', {
				data: {
					user_id: this.user_id,
					type: '0'
				}
			}).then(res=>{
				if (res.errno == '0') {
					this.type = '0';
					this.maskShow = false;
					this.sucResShow = true;
				} else {
					wx.showToast({
						title: res.errmsg,
						icon: 'none',
						duration: 2000,
					});
				}
			});
		},
		showChangeCash() {
			if(this.toCashNum > 0) {
				Net.get('Sakura.userExchange', {
					data: {
						user_id: this.user_id,
						type: '1'
					}
				}).then(res=>{
					if (res.errno == '0') {
						this.type = '1';
						this.maskShow = true;
						this.sucResShow = true;
						Net.newLog(
							{
								mt: 'exchange_money',
							},
							this.logCommonParam,
						);
					} else {
						wx.showToast({
							title: res.errmsg,
							icon: 'none',
							duration: 2000,
						});
					}
					
				});
			} else {
				wx.showToast({
					title: '无可兑换金额',
					icon: 'none',
					duration: 2000,
				})
			}
			
		},
		closeAlert () {
			this.maskShow = false;
		}
	}
};
</script>

<style scoped>
button::after{
	display: none;
}
body {
	color: #191919;
}
.my-sakura-box {
	display: flex;
	justify-content: center;
}
.my-sakura {
	width: auto;
	height: 25px;
	margin: 3px;
	padding-left: 30px;
  color: rgb(214, 35, 35);
	background: url('https://s.wandougongzhu.cn/s/7a/513_d24f95.png') no-repeat;
	background-size: 25px;
	background-position: left center;
}
.btn-box {
	display: flex;
	flex-direction:row;
	justify-content:space-around;

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
.mysakura-btn,.suc-btn {
	bottom: 10px;
	width: 100px;
	height: 35px;
	line-height: 35px;
	font-size: 14px;
	color: #fff;
	background: url('https://s5.wandougongzhu.cn/s/2a/btn_e2760e.jpg') no-repeat;
	background-size: 100% 100%;
	margin: 0 auto;
}
.suc-btn {
	margin-top: 10px;
}
.dis-btn {
	background: url('https://s3.wandougongzhu.cn/s/28/_67a6fa.png') no-repeat;
	background-size: 100% 100%;
}
.to-alert-box {
	position: absolute;
	left: 50%;
	top: 50%;
	transform: translate(-50%,-50%);
	width: 280px;
	height: 172px;
	font-size: 14px;
	text-align: center;
	background: url('https://s4.wandougongzhu.cn/s/a2/alert_s_f4973c.png') no-repeat;
	background-size: 100% 100%;
}
.to-cash-tip {
	width: 200px;
	height: 60px;
	margin: 0 auto;
}
.changecash-title {
	margin-top: 10px;
}
#mask,#suc {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	background: rgba(0,0,0,.7);
}
#suc {
	text-align: center;
	background: url('https://s4.wandougongzhu.cn/s/6b/duihuan_d99279.jpg') no-repeat;
	background-size: 100% 100%;
}
#suc .suc-title {
	font-size: 22px;
	margin-top: 90px;
  color: rgb(216, 35, 35);
	/* -webkit-text-stroke:1rpx #ffffff; */
	text-align:center;
	font-weight:bold;
}
#suc .suc-tips {
	width: 300px;
	margin: 5px auto;
	font-size: 14px;
	color: #191919;
  color: rgb(22, 40, 84);
}

#suc .suc-res {
	font-size: 32px;
  color: rgb(216, 35, 35);
	font-weight: bold;
	margin: 20px auto 5px auto;
}
.suc-banner {
	width: 315px;
	height: 200px;
	background: url('https://s5.wandougongzhu.cn/s/98/banner_c52dba.jpg') no-repeat;
	background-size: contain;
	margin: 10px auto;
}
.suc-res span {
	font-size: 12px;
}
.suc-btn {
	display: block;
}
.container {
	font-weight: bold;
	position: absolute;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	text-align: center;
	background: url('https://s1.wandougongzhu.cn/s/19/_5f3df6.jpg') no-repeat;
	background-size: 100% 100%;
	background-color: #f3f2f1;
}
.mysakura-tips {
	width: 230px;
	height: 60px;
	font-weight: normal;
	margin: 10px auto;
}
.mysakura {
	width: 15px;
	height: 15px;
	margin: 3px auto;
	background: url('https://s3.wandougongzhu.cn/s/7e/4_88421d.png') no-repeat;
	background-size: cover;
}
.none-tips {
	font-size: 14px;
	color: rgb(111,111,111);
}
.min-tips {
	font-size: 12px;
	color: rgb(111,111,111);
	margin-top: 10px;
}
.duihuan-box {
	width: 100%;
	height: 300px;
	display: flex;
	flex-direction: column;
	justify-items: center;
	align-items: center;
	justify-content: center;
}
.cash-box,.score-box {
	width: 275px;
	height: 80px;
	border-radius: 4px;
	overflow: hidden;
	background: url('https://s5.wandougongzhu.cn/s/52/xianjinbtn_254e29.png') no-repeat;
	background-size: 100% 100%;
	color: #ffffff;
	position: relative;
}
.cash-box .icon ,.score-box .icon{
	width: 35px;
	height: 20px;
	position: absolute;
	left: -5px;
	top: -2px;
}
.score-box {
	margin-top: 20px;
}
.cash-rate {
	width: 60px;
	height: 25px;
	position: absolute;
	left: 140px;
	font-size: 14px;
  color: rgb(216, 40, 40);
	-webkit-transform: rotate(20deg);
	transform: rotate(20deg);
	line-height: 25px;
	background: url(https://s2.wandougongzhu.cn/s/cb/_0182ea.png) no-repeat;
	background-size: 100%;
}
.cash-content,.score-content {
	display: flex;
	align-items: center;
	justify-content: center;
}
.score-box {
	background: url('https://s4.wandougongzhu.cn/s/a4/_39ec92.png') no-repeat;
	background-size: 100% 100%;
}
.tips2 {
	font-size: 12px;
	color: #fff;
	width: 170px;
	height: 50px;
	text-align: center;
}
.tips2 span {
	font-size: 23px;
}
.mini-tip {
	font-size: 12px;
}
.tips {
	position: relative;
	font-size: 20px;
	font-weight: bold;
  color: rgb(22, 40, 84);
	text-align: center;
	margin-top: 100px;
}
.to-cash-btn,.to-score-btn,.to-cash-btn-disable {
	width: 80px;
	height: 30px;
	font-size: 12px;
	line-height: 30px;
	color: rgb(63, 4, 4);
	margin: 25px auto;
	background: url('https://s5.wandougongzhu.cn/s/f8/ing_fe1225.png') no-repeat;
	background-size: 100% 100%;
}
.to-cash-btn-disable {
	color: #a96301;
	background: url('https://s4.wandougongzhu.cn/s/de/2_aea31a.png') no-repeat;
	background-size: 100% 100%;
}
#mask {
	/* visibility: hidden; */
	text-align: center;
	display: flex;
	justify-content: center;
	align-items: center;
}
</style>

