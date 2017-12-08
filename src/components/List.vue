<template>
  <div class="wraper">
    <div class="tools">
      <div class="tool-cter">
        <button class="tool page-up" @click="pageupClick" :class="{'tool-dis':pageIndex == 1 || pageClicked}"></button>
        <button class="tool page-down" @click="pagedownClick" :class="{'tool-dis':pageClicked}"></button>
        <router-link :to="{ name: 'main', params: {} }"><button class="tool page-home"></button></router-link>
      </div>
    </div>
    <div class="list-cter">
      <transition-group
        v-show="!isup"
        tag="ul"
        name="flipc"
        appear
        mode="out-in"
        enter-active-class="animated fadeInUp"
        leave-active-class="animated fadeOutUp">
        <li v-for="item in listData" :key="item.id" @click="goDetail(item)">
          <div><img :src="item.imagePath" /></div>
          <p>{{item.title}}</p>
          <span>¥ {{item.price}}</span>
        </li>
      </transition-group>
      <transition-group
        v-show="isup"
        tag="ul"
        name="flipc"
        appear
        mode="out-in"
        enter-active-class="animated fadeInDown"
        leave-active-class="animated fadeOutDown">
        <li v-for="item in listData" :key="item.id" @click="goDetail(item)">
          <div><img :src="item.imagePath" /></div>
          <p>{{item.title}}</p>
          <span>¥ {{item.price}}</span>
        </li>
      </transition-group>
    </div>
  </div>
</template>
<script>
export default {
  data () {
    return {
      listData: [],
      pageIndex: this.$route.params.pageIndex,
      pageSize: 9,
      isup: false,
      pageClicked: false
    }
  },
  watch: {
    '$route': 'fetchData'
  },
  created () {
    this.fetchData()
  },
  methods: {
    goDetail (item) {
      this.$router.push('/detail')
    },
    fetchData () {
      for (let i = (this.pageIndex - 1) * this.pageSize; i < this.pageIndex * this.pageSize; i++) {
        this.listData.push({id: i, title: `PSV200${i} 黑色 64G`, price: '2488', imagePath: '/static/images/prosmall.png'})
      }
    },
    pagedownClick () {
      if (!this.pageClicked) {
        this.isup = false
        this.listData = []
        this.pageIndex++
        this.pageClicked = true
        // animationend transitionend
        setTimeout(() => {
          this.pageClicked = false
          this.$router.push({name: 'list', params: {pageIndex: this.pageIndex}})
        }, 1000)
      }
    },
    pageupClick () {
      if (this.pageIndex > 1 && !this.pageClicked) {
        this.isup = true
        this.listData = []
        this.pageIndex--
        this.pageClicked = true
        setTimeout(() => {
          this.pageClicked = false
          this.$router.push({name: 'list', params: {pageIndex: this.pageIndex}})
        }, 1000)
      }
    }
  }
}
</script>
<style lang="less" scoped>
.list-cter {
  width: 702px;
  ul {
    margin: 100px 15px;
    // &::after {content: ''; display: block; height: 0; visible:hidden; clear: both;}
    li {
      width: 200px;
      height: 330px;
      background: #384267;
      box-shadow: 0 0 15px #343961;
      float: left;
      margin-left: 24px;
      margin-top: 36px;
      border-radius: 15px;
      box-sizing: content-box;
      div {
        background: #afb3c2;
        width: 190px;
        height: 210px;
        margin: 24px auto 10px;
      }
      p {
        display: block;
        width: 190px;
        line-height: 22px;
        height: 22px;
        margin: 0 auto;
        color: #b0b5c3;
        padding-left: 15px;
        overflow: hidden;
        font-size: 20px;
        text-overflow:ellipsis;
        white-space: nowrap;
      }
      span {
        display: block;
        width: 190px;
        height: 30px;
        line-height: 30px;
        margin: 8px auto;
        color: #fff;
        font-size: 30px;
        text-indent: 15px;
      }
    }
  }
}
.flipc-move {
  transition: transform 1s;
}
</style>
