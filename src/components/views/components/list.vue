<template>
<div>
    <div class="link">
      <div class="img">
        <img :src="listArr.img" alt="">
      </div>
      <div class="content">
        <p class="name"><a :href="listArr.url">{{listArr.project_name}}</a></p>
        <p class="owner">
          <span style="padding-right: 15px">网站负责人：{{listArr.project_develop_m}}</span>
          <span>产品负责人：{{listArr.project_product_m}}</span>
        </p>
        <p class="font" :title="listArr.project_des">{{listArr.project_des}}</p>
      </div>
      <div class="foot">
        <span class="right">
          <span @click="collect(listArr)">
            <img src="static/images/collection.png" alt="" class="collection" v-if="!listArr.isCollect" >
            <img src="static/images/done.png" alt="" v-else  class="collection">
          </span>
        </span>
      </div>
    </div>
</div>
</template>

<script>
export default {
  name: 'list',
  data () {
    return {
      ArrList: []
    }
  },
  props: {
    listArr: {
      type: Object,
      default: () => {}
    },
    isCollect: {
      type: Boolean
    }
  },
  methods: {
    collect (item) {
      item.isCollect = !item.isCollect
      this.$emit('add', item)
    }
  }
}
</script>

<style scoped>
.link{
  display: block;
  width: 100%;
  height: 355px;
}
.img{
  height: 202px;
  overflow: hidden;
}
.img img{
  display: block;
  height: 202px;
  width: 310px;
  transition: all .6s;
}
.img img:hover{
  transform: scale(1.05);
}
.content{
  padding: 10px 15px;
  border-top: 0;
}
.font{
  /*height: 48px;*/
  line-height: 24px;
  overflow: hidden;
  font-size: 14px;
  margin-top: 8px;
  color: #636363;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
}
.name{
  color: black;
}
.owner{
  font-size: 12px;
  padding-top: 10px;
}
.foot{
  overflow: hidden;
  padding: 0 15px;
}
.right{
  float: right;
}
.collection{
  width: 20px;
  height: 20px;
  cursor: pointer;
}
</style>
