<template>
  <div @click="clickHandle">

    <div id="topBanner" class="slide">
      <div class="slideShow">
        <ul>
          <transition-group tag="url" name="image">
            <li v-for="(item, index) in bannerList" :key="index" v-show="index === mark">
              <a href="#">
                <img :src="item">
              </a>
            </li>
          </transition-group>
        </ul>
      </div>
      <div class="bar">
        <span v-for="(val, idx) in bannerList" :key="idx" :class="{ 'active':idx===mark }" @click="change(idx)"></span>
      </div>
    </div>

    <div class="userinfo" @click="bindViewTap">
      <img class="userinfo-avatar" v-if="userInfo.avatarUrl" :src="userInfo.avatarUrl" background-size="cover" />
      <img class="userinfo-avatar" src="/static/images/user.png" background-size="cover" />

      <div class="userinfo-nickname">
        <card :text="userInfo.nickName"></card>
      </div>
    </div>

    <div class="usermotto">
      <div class="user-motto">
        <card :text="motto"></card>
      </div>
    </div>

    <form class="form-container">
      <input type="text" class="form-control" :value="motto" placeholder="v-model" />
      <input type="text" class="form-control" v-model="motto" placeholder="v-model" />
      <input type="text" class="form-control" v-model.lazy="motto" placeholder="v-model.lazy" />
    </form>

    <!-- 使用 click-counter 组件 -->
    <click-counter />

    <a href="/pages/counter/main" class="counter">去往Vuex示例页面</a>

    <div class="all">
        <div class="left">
        </div>
        <div class="right">
        </div>
    </div>
  </div>
</template>

<script>
import card from '@/components/card'
// 导入组件
import ClickCounter from '@/components/click-counter'

export default {
  data () {
    return {
      motto: 'Hello miniprograme',
      userInfo: {
        nickName: 'mpvue',
        avatarUrl: 'http://mpvue.com/assets/logo.png'
      },
      mark: 0,
      bannerList: ['/static/images/beautiful-1.jpeg', '/static/images/beautiful-2.jpeg', '/static/images/beautiful.jpeg', '/static/images/cleaner-1.jpeg']
    }
  },

  components: {
    card,
    ClickCounter
  },

  methods: {
    bindViewTap () {
      const url = '../logs/main'
      if (mpvuePlatform === 'wx') {
        mpvue.switchTab({ url })
      } else {
        mpvue.navigateTo({ url })
      }
    },
    clickHandle (ev) {
      console.log('clickHandle:', ev)
      // throw {message: 'custom test'}
    },
    // 自动轮播
    autoPlay () {
      this.mark++
      console.log(this.mark, 'mark的')
      if (this.mark === 3) {
        this.mark = 0
      }
    },
    play () {
      setInterval(this.autoPlay, 2500)
    },
    change (i) {
      this.mark = i
    }
  },

  created () {
    // let app = getApp()
    this.play()
  }
}
</script>

<style scoped>
.userinfo {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.userinfo-avatar {
  width: 128rpx;
  height: 128rpx;
  margin: 20rpx;
  border-radius: 50%;
}

.userinfo-nickname {
  color: #aaa;
}

.usermotto {
  margin-top: 150px;
}

.form-control {
  display: block;
  padding: 0 12px;
  margin-bottom: 5px;
  border: 1px solid #ccc;
}
.all{
  width:7.5rem;
  height:1rem;
  background-color:blue;
}
.all:after{
  display:block;
  content:'';
  clear:both;
}
.left{
  float:left;
  width:3rem;
  height:1rem;
  background-color:red;
}

.right{
  float:left;
  width:4.5rem;
  height:1rem;
  background-color:green;
}
/* 轮播图 */
* {
  margin: 0;
  padding: 0;
  list-style: none;
}
.slide {
  width: 100%;
  height: 150px;
  margin: 0 auto;
  overflow: hidden;
  position: relative;
}
.slideShow, .slideShow ul, .slideShow ul li {
  width: 100%;
  height: 150px;
}
li {
  position: absolute;
}
.slideShow img {
  width: 100%;
  height: 150px;
}
.bar {
  position: absolute;
  width: 100%;
  bottom: 10px;
  margin: 0 auto;
  z-index: 10;
  text-align: center;
}
.bar span {
  width: 5px;
  height: 5px;
  border: 1px solid transparent;
  border-radius: 50%;
  background-color: #ffffff;
  display: inline-block;
  margin-right: 10px;
}
.active {
  background-color: #bfd6b6 !important;
}
/* 动画效果 */
.image-enter-active {
  transform: translateX(0);
  transition: all 1.5s ease;
}
.image-leave-active {
  transform: translateX(-100%);
  transition: all 1.5s ease;
}
.image-enter {
  transform: translateX(100%);
}
.image-leave {
  transform: translateX(0);
}
</style>
