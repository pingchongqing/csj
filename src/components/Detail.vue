<template>
  <div class="wraper">
    <div class="tools">
      <div class="tool-cter">
        <button class="tool back" @click="backClick"></button>
        <button class="tool userlogin" ></button>
        <router-link :to="{ name: 'main', params: {} }"><button class="tool page-home"></button></router-link>
      </div>
    </div>
    <div class="detail-cter">
      <transition
        appear
        enter-active-class="animated delay1 slideInDown"
        leave-active-class="animated fadeOutDown"
      >
        <div class="detail box" :class="{'notchecked': isBuy}">
          <div class="picbox">
            <img :src="detail.imagePath" />
            <div class="titleline">
              <p>{{detail.title}}</p>
              <span>¥{{detail.price}}</span>
            </div>
          </div>
          <div class="info">
            <p>{{detail.info}}</p>
          </div>
          <div class="paychoilce">
            <div class="checkgroup">
              <input type="radio" name="alipay"  :checked="paychecked == 'alipay'" @change="radioChange"  />
              <span class="paybox" :class="{'checked': paychecked == 'alipay'}" @click="paycheck('alipay')">
                <img src="~images/alipay.jpg" />
              </span>
            </div>
            <div class="checkgroup">
              <input type="radio" name="weipay" :checked="paychecked == 'weipay'" @change="radioChange" />
              <span class="paybox" :class="{'checked': paychecked == 'weipay'}" @click="paycheck('weipay')">
                <img src="~images/weipay.jpg" />
              </span>
            </div>
          </div>
          <div class="submit" @click="buyClick">
            立即购买
          </div>
        </div>
      </transition>
      <transition
        appear
        enter-active-class="animated delay slideInDown"
        leave-active-class="animated slideOutDown"
      >
        <div class="alipay box" :class="{checked: paychecked == 'alipay' && isBuy}">
          <div class="qrcodebox alipay">
            <img src="~images/qrcode.jpg" />
            <p class="tip">请扫描上方二维码完成支付~</p>
          </div>
        </div>
      </transition>
      <transition
        appear
        enter-active-class="animated slideInDown"
        leave-active-class="animated slideOutDown"
      >
        <div class="weipay box" :class="{checked: paychecked == 'weipay' && isBuy, notchecked: paychecked != 'weipay' && isBuy}">
          <div class="qrcodebox weipay">
            <img src="~images/qrcode.jpg" />
            <p class="tip">请扫描上方二维码完成支付~</p>
          </div>
        </div>
      </transition>
    </div>
  </div>
</template>
<script>
export default {
  data () {
    return {
      detail: {
        title: 'iPhoneX 256G 黑色',
        price: 9688,
        imagePath: '/static/images/probig.png',
        info: '商品名称：AppleiPhone X商品编号：5089237商品毛重：440.00g商品产地：中国大陆系统：苹果（IOS）'
      },
      paychecked: 'alipay',
      isBuy: false
    }
  },
  methods: {
    paycheck (s) {
      this.paychecked = s
    },
    buyClick () {
      this.isBuy = true
    },
    backClick () {
      if (this.isBuy) {
        this.isBuy = false
      } else {
        this.$router.push('/list/1')
      }
    },
    radioChange (e) {
      this.paycheck(e.target.name)
      console.log(e.target.name)
    }
  }
}
</script>
<style lang="less">
.delay {
  animation-delay: .1s
}
.delay1 {
  animation-delay: .2s
}
.detail-cter {
  width: 702px;
  position: relative;
  height: 1366px;
  .box {
    height: 890px;
    position: absolute;
    top: 50%;
    left: 50%;
    border-radius: 20px;
    box-shadow: 0 10px 30px #232c49;
    &.detail {
      width: 640px;
      background: #384267;
      z-index: 66;
      margin-left: -320px;
      margin-top: -450px;
      transition: all .5s;
      &.notchecked {
        width: 560px;
        margin-left: -280px;
        margin-top: -470px;
        z-index: 64;
      }
      .picbox {
        height: 516px;
        background: #232b47;
        border-top-left-radius: 20px;
        border-top-right-radius: 20px;
        text-align: center;
        img {
          max-width: 100%;
          max-height: 460px;
        }
        .titleline {
          height: 55px;
          background: rgba(255,255,255,.15);
          padding: 0 12px;
          font-size: 20px;
          line-height: 55px;
          p {
            float: left;
            color: #fff;
          }
          span {
            float: right;
            color: #ed5858;
          }
        }
      }
      .info {
        color: #f6f6f6;
        padding: 20px;
        text-align: left;
        line-height: 180%;
        height: 150px;
        font-size: 18px;
      }
      .paychoilce {
        height: 155px;
        padding: 10px 25px;
        .checkgroup {
          float: left;
          margin-right: 30px;
          position: relative;
          input[type="radio"] {
            position: absolute;
            top: 50%;
            transform: translate(0, -50%);
          }
          .paybox {
            padding: 10px;
            background: #fff;
            display: block;
            margin-left: 22px;
            transition: all .5s;
            text-align: center;
            img {
              width: 75%;
            }
            &.checked {
              box-shadow: 0 0 15px #ff5656 inset;
            }
          }
        }
      }
      .submit {
        cursor: pointer;
        height: 100px;
        position: absolute;
        line-height: 100px;
        color: #ed5858;
        text-align: center;
        width: 100%;
        bottom: 0;
        border-top: #303b5a 1px solid;
        border-bottom-left-radius: 20px;
        border-bottom-right-radius: 20px;
        font-size: 20px;
      }
    }
    .qrcodebox {
      height: 316px;
      &.weipay {background: #45c01a;}
      &.alipay {background: #10aeef;}
      border-top-left-radius: 20px;
      border-top-right-radius: 20px;
      text-align: center;
      img {
        max-width: 100%;
        max-height: 460px;
        margin-top: 150px;
        box-shadow: 0 0 20px #bacef1;
      }
      .tip {
        text-align: center;
        margin-top: 120px;
        display: block;
        font-size: 18px;
        color: #fff;
      }
    }
    &.alipay {
      width: 600px;
      background: #384267;
      z-index: 65;
      margin-left: -300px;
      margin-top: -460px;
      transition: all .5s;
      &.checked {
        width: 640px;
        z-index: 66;
        margin-left: -320px;
        margin-top: -450px;
      }
    }
    &.weipay {
      width: 560px;
      background: #384267;
      z-index: 64;
      margin-left: -280px;
      margin-top: -470px;
      transition: all .5s;
      &.notchecked {
        width: 600px;
        z-index: 65;
        margin-left: -300px;
        margin-top: -460px;
      }
      &.checked {
        width: 640px;
        z-index: 66;
        margin-left: -320px;
        margin-top: -450px;
      }
    }

  }
}
</style>
