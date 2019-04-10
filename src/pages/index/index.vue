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

    <div class="tab-content">
      <ul class="nav">
        <li v-for="(item, index) in navList" :key="index" @click="menuShow(index)"><img :src="item.image" /><a v-text="item.name" :class="{active:!(index - menuIndex)}"></a></li>
      </ul>
      <div class="detail-content clearfix">
        <div v-for="(item, index) in contentList[menuIndex]" :key="index">
          <detail-content :list="item"></detail-content>
        </div>
      </div>
    </div>

    <!-- <div class="userinfo" @click="bindViewTap">
      <img class="userinfo-avatar" v-if="userInfo.avatarUrl" :src="userInfo.avatarUrl" background-size="cover" />
      <img class="userinfo-avatar" src="/static/images/user.png" background-size="cover" />

      <div class="userinfo-nickname">
        <card :text="userInfo.nickName"></card>
      </div>
    </div> -->

    <!-- <div class="usermotto">
      <div class="user-motto">
        <card :text="motto"></card>
      </div>
    </div> -->

    <!-- <form class="form-container">
      <input type="text" class="form-control" :value="motto" placeholder="v-model" />
      <input type="text" class="form-control" v-model="motto" placeholder="v-model" />
      <input type="text" class="form-control" v-model.lazy="motto" placeholder="v-model.lazy" />
    </form> -->

    <!-- 使用 click-counter 组件 -->
    <!-- <click-counter /> -->

    <!-- <a href="/pages/counter/main" class="counter">去往Vuex示例页面</a> -->

    <!-- <div class="all">
        <div class="left">
        </div>
        <div class="right">
        </div>
    </div> -->
  </div>
</template>

<script>
import card from '@/components/card'
// 导入组件
import ClickCounter from '@/components/click-counter'
import detailContent from '@/components/detail-content'

export default {
  data () {
    return {
      motto: 'Hello miniprograme',
      userInfo: {
        nickName: 'mpvue',
        avatarUrl: 'http://mpvue.com/assets/logo.png'
      },
      mark: 0,
      bannerList: ['/static/images/beautiful-1.jpeg', '/static/images/beautiful-2.jpeg', '/static/images/beautiful.jpeg', '/static/images/cleaner-1.jpeg'],
      menuIndex: 0,
      navList: [
        {
          name: '推荐',
          image: '/static/images/番剧推荐.png'
        },
        {
          name: '美容',
          image: '/static/images/美容仪.png'
        },
        {
          name: '美甲',
          image: '/static/images/美甲.png'
        },
        {
          name: '美发',
          image: '/static/images/美发素.png'
        },
        {
          name: '美睫',
          image: '/static/images/美睫.png'
        }
      ],
      contentList: {
        0: [
          {
            avatar: '/static/images/beautiful-1.jpeg',
            title: '秋季自然特价美甲',
            price: '198',
            desc: '我们追求的是没有最长只有更长！'
          },
          {
            avatar: '/static/images/beautiful-2.jpeg',
            title: '睫毛稀疏中睫毛来帮忙',
            price: '1888',
            desc: '我们追求的是没有最长只有更长！'
          },
          {
            avatar: '/static/images/beautiful-1.jpeg',
            title: '爱丽克EricParisSalon',
            price: '1588',
            desc: '我们追求的是没有最长只有更长！'
          },
          {
            avatar: '/static/images/beautiful-1.jpeg',
            title: '伊本造型',
            price: '198',
            desc: '伊本造型是由著名形象设计师杨昊明主导的时尚沙龙'
          },
          {
            avatar: '/static/images/beautiful.jpeg',
            title: '画对了妆，微微一笑颜值倍增',
            price: '198',
            desc: '《微微一笑很倾城》的剧照简直简直简直简直简直'
          }
        ],
        1: [
          {
            avatar: '/static/images/beautiful-1.jpeg',
            title: '爱丽克EricParisSalon',
            price: '1588',
            desc: '我们追求的是没有最长只有更长！'
          },
          {
            avatar: '/static/images/beautiful.jpeg',
            title: '画对了妆，微微一笑颜值倍增',
            price: '198',
            desc: '《微微一笑很倾城》的剧照简直简直简直简直简直'
          }
        ],
        2: [
          {
            avatar: '/static/images/beautiful-1.jpeg',
            title: '秋季自然特价美甲',
            price: '198',
            desc: '我们追求的是没有最长只有更长！'
          }
        ],
        3: [
          {
            avatar: '/static/images/beautiful-1.jpeg',
            title: '伊本造型',
            price: '198',
            desc: '伊本造型是由著名形象设计师杨昊明主导的时尚沙龙'
          }
        ],
        4: [
          {
            avatar: '/static/images/beautiful-2.jpeg',
            title: '睫毛稀疏中睫毛来帮忙',
            price: '1888',
            desc: '我们追求的是没有最长只有更长！'
          }
        ]
      }
    }
  },

  components: {
    card,
    ClickCounter,
    detailContent
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
      if (this.mark === 3) {
        this.mark = 0
      }
    },
    play () {
      setInterval(this.autoPlay, 2500)
    },
    change (i) {
      this.mark = i
    },
    menuShow (i) {
      this.menuIndex = i
      console.log(this.menuIndex, '234')
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
.slideShow ul li {
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
.bar span.active {
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
/* nav */
.tab-content {
  margin-top: 15px;
}
.tab-content, .tab-content ul {
  width: 100%;
  height: 30px;
}
.clearfix:after {
  visibility: hidden;
  display: block;
  font-size: 0;
  content: " ";
  clear: both;
  height: 0;
}
.tab-content ul li {
  float: left;
  width: 20%;
  height: 50px;
  text-align: center;
  font-size: 14px;
}
.tab-content ul li img {
  display: inline-block;
  width: 30px;
  height: 30px;
}
.tab-content ul li a {
  color: #ccc;
}
.tab-content ul li a.active {
  color: #323333;
}
.detail-content {
  margin-top: 30px;
}
</style>
