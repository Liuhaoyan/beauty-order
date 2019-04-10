<template>
  <div class="order-detail">
      <img :src="image"/>
      <div class="order-information">
          <form class="form-container">
              <label for="name">姓名</label><input type="text" class="form-control" placeholder="请填写姓名" />
              <label for="name">电话</label><input type="text" class="form-control" placeholder="请填写电话" />
              <label for="name">服务时间</label><input type="date" class="form-control"/>
              <label for="name">留言信息</label><input type="textarea" class="form-control" placeholder="输入信息" />
          </form>
      </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      image: '',
      motto: ''
    }
  },
  methods: {
  },
  mounted () {
    console.log(this.$root.$mp.query, 654)
    this.image = this.$root.$mp.query.img
  }
}
</script>

<style scoped>
.order-detail img {
    width: 100%;
    height: 150px;
}
.order-information {
    padding: 10px 20px;
}
</style>
