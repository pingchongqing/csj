<template>
  <div id="app" :style="{zoom:zoom}">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      zoom: 1
    }
  },
  created () {
    this.$nextTick(() => {
      console.log(window.screen.availHeight)
    })
    this.zoom = window.screen.availHeight / 1382 - 0.101
  }
}
</script>

<style src="@/assets/css/base.less" lang="less"></style>
<style src="@/assets/css/animate.css" ></style>
<style lang="less">
.wraper {
  width: 768px;
  height: 1366px;
  background: url('~images/bg.jpg');
  background-size: cover;
  border-top: #000 8px solid;
  border-bottom: #000 8px solid;
  border-left: #000 24px solid;
  border-right: #000 24px solid;
  margin: 0 auto;
  box-sizing: content-box;
  box-shadow: 0 0 10px #000;
  position: relative;
  overflow: hidden;
  margin: 20px auto;
}
.tools {
  width: 50px;
  height: 1366px;
  float: right;
  position: relative;
  margin: 0 8px;
  .tool-cter {
    position: absolute;
    top: 50%;
    transform: translate(0,-50%);
  }
  .tool-dis {opacity: .3;}
  .tool {
    transition: all .3s;
    width: 50px;
    height: 50px;
    background: url('~images/tools.png') no-repeat;
    background-size: 100%;
    display: block;
    margin: 20px 0;
    &.page-down {
      background-position: 0 -50px;
    }
    &.back {
      background-position: 0 -150px;
    }
    &.userlogin {
      background-position: 0 -100px;
    }
    &.page-up {
      background-position: 0 0;
    }
    &.page-home {
      background-position: 0 -200px;
    }
  }
}
</style>
