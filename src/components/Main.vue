<template>
  <div class="wraper">
    <transition enter-active-class="animated fadeIn" leave-active-class="animated fadeOut" appear>
      <div class="main-img" @click="mainClick">
        <img src="~images/main.jpg" />
      </div>
    </transition>
    <div class="btn-cter" v-show="maskShow">
      <router-link :to="{ name: 'list', params: {pageIndex: 1} }"><button class="btn buy">购买手机</button></router-link>
      <button class="btn card">新卡套餐</button>
      <button class="btn card">补卡业务</button>
    </div>
    <div class="mask" v-show="maskShow" @click="maskClick"></div>
  </div>
</template>
<script>
export default {
  name: 'main',
  data () {
    return {
      maskShow: false
    }
  },
  methods: {
    mainClick () {
      this.maskShow = true
    },
    maskClick () {
      this.maskShow = !this.maskShow
    }
  }
}
</script>
<style scoped lang="less">
@keyframes maskmove {
  from {opacity: 0}
  to {opacity: .75}
}
.mask {
  animation: maskmove .3s;
  background: #000;
  position: absolute;
  z-index: 50;
  width: 768px;
  height: 1366px;
  opacity: .75;
  top:0;
  left: 0;
}
.btn-cter {
  position: absolute;
  z-index: 51;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
@keyframes btnmove {
  from {transform: translateX(30px); opacity: 0}
  to {transform: translateX(0); opacity: 1}
}
.btn {
  width: 255px;
  height: 65px;
  border-radius: 8px;
  font-size: 20px;
  display: block;
  margin: 3px auto;
  &.buy {
    background: linear-gradient(#1fb3e3 0%, #16aada 50%, #0b9fcf 51%, #0094c4 100%);
    border-top: #8ce2ff 1px solid;
    color: #fff;
    animation: btnmove .5s;
  }
  &.card {
    background: linear-gradient(#f4f4f4 0%, #efefef 50%, #eaeaea 51%, #e5e5e5 100%);
    color: #1fb3e3;
    border-top: #fff 1px solid;
    animation: btnmove .8s;
  }
}

</style>
