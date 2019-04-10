<template>
  <div class="pro-content">
    <div class="avatar">
        <img :src="list.avatar" />
    </div>
    <div class="detail-product">
        <div class="pro-title">{{ list.title }}</div>
        <div class="pro-price">价格：¥{{ list.price }}</div>
        <div class="pro-desc">{{ list.desc }}</div>
    </div>
    <div class="order-operation">
        <div @click="handleOrder(list.title, list.avatar)">预约</div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['list'],
  data () {
    return {
    }
  },
  methods: {
    handleOrder (title, img) {
      console.log('点击预约跳转到详情页')
      const url = '/pages/detail/main?title=' + title + '&img=' + img
      console.log(url)
      wx.navigateTo({ url })
    }
  },
  mounted () {
    console.log(this.list, 23)
  }
}
</script>


<style scoped>
/* tab详情 */
.pro-content {
  width: 100%;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.pro-content .avatar, .pro-content .order-operation {
  flex: 1;
}
.pro-content .detail-product {
  flex: 4;
}
.pro-content .avatar {
  margin: 0 10px 0 15px;
}
.pro-content .order-operation {
  margin: 0 15px 0 10px;
}
.pro-content .avatar img {
  display: inline-block;
  width: 80px;
  height: 80px;
}
.pro-content .pro-title {
  font-size: 18px;
}
.pro-content .pro-price {
  font-size: 18px;
  color: #f00;
  margin-top: 6px;
}
.pro-content .pro-desc {
  font-size: 14px;
  color: #ccc;
}
.pro-content .pro-desc, .pro-content .pro-title {
  max-width: 200px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.order-operation div {
  font-size: 14px;
  width: 30px;
  height: 30px;
  padding: 5px;
  text-align: center;
  line-height: 30px;
  background-color: #ff5151;
  color: #fff;
  border-radius: 50%;
}
</style>

