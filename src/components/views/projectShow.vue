<template>
  <div class="project">
    <div class="header">
      <div class="header-con">
        <div class="header-left">
          <img src="../../assets/images/logo1.png" alt="" class="logo">
          <div class="slogan">这里是文字这里是文字,这里是文字这里是文字</div>
        </div>
        <div class="header-right">
          <input type="search" class="ipu" placeholder="请输入项目名称">
          <img src="../../assets/images/search.png" class="search"/>
        </div>
      </div>
    </div>
    <div class="main">
      <div class="list">
        <ul class="ulFrame">
          <li v-for="item in list" :key="item.id" class="item">
            <list :listArr="item" @add="addCollect"></list>
          </li>
        </ul>
      </div>
    </div>
    <footer>Copyright © 2020 JD.COM 京东版权所有 Powered by 商业中台组</footer>
  </div>
</template>

<script>
import list from './components/list'
const ERR_OK = 0
export default {
  name: 'ProjectShow',
  data () {
    return {
      list: [],
      arr: []
    }
  },
  created () {
    this.$http.get('/api/list').then((response) => {
      let datas = response.data
      console.log(datas)
      if (datas.erron === ERR_OK) {
        let dataJson = datas.data
        let arr1 = JSON.parse(localStorage.getItem('arr'))
        console.log(arr1)
        if (arr1 && arr1.length) {
          dataJson.forEach((item) => {
            if (arr1.includes(item.id)) {
              item.isCollect = true
            }
          })
        }
        this.list = dataJson
      }
    })
      .catch(function (error) {
        console.log('出错喽：' + error)
      })
  },
  methods: {
    // 收藏
    addCollect (item) {
      let get = JSON.parse(localStorage.getItem('arr'))
      console.log(get)
      if (item.isCollect === true) {
        if (get) {
          if (get.includes(item.id)) {
            console.log('我在')
          } else {
            get.push(item.id)
            localStorage.setItem('arr', JSON.stringify(get))
          }
        } else {
          get.push(item.id)
          localStorage.setItem('arr', JSON.stringify(get))
        }
      } else {
        get.splice(get.findIndex(item => item === item.id) + 1, 1)
        localStorage.setItem('arr', JSON.stringify(get))
      }
    }
  },
  components: {
    list
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.project{
  width: 100%;
  position: relative;
  background-image: url("../../assets/images/3.jpeg");
  background-attachment: fixed;
  background-size: cover;
  background-position: 0;
}
.header{
  position: sticky;
  top: 0;
  left: 0;
  width: 100%;
  height: 80px;
  line-height: 80px;
  background-color: #2c3e50;
  color: #fff;
  padding: 10px 0;
  z-index: 99;
}
.header-con{
  width: 80%;
  margin: 0 auto;
  overflow: hidden;
}
.header-left{
  float: left;
}
.logo{
  width: 55px;
  height: 55px;
  display: inline-block;
  vertical-align: middle;
}
.slogan{
  display: inline-block;
  padding-left: 10px;
}
.header-right{
  float: right;
  position: relative;
}
.ipu{
  padding: 10px;
  width: 300px;
  border: none;
  border-radius: 5px;
}
.ipt:focus{
  border: 1px solid darkseagreen;
}
.search{
  position: absolute;
  right: 15px;
  top: 30px;
  width: 20px;
  height: 20px;
}
.wall{
  height: 600px;
  overflow: hidden;
}
.wall_pic{
  width: 100%;
  max-height: 100%;
  background-repeat: no-repeat;
  background-position: top center;
  background-size: cover;
  background-attachment: fixed;
}
.main{
  padding-bottom: 100px;
}
footer{
  position: absolute;
  bottom: 0;
  right: 0;
  display: block;
  text-align: center;
  background-color: #3c3d41;
  color: #a4a7b3;
  line-height: 50px;
  height: 50px;
  font-size: 12px;
  width: 100%;
}

.list{
  width: 1020px;
  margin: 0 auto;
  overflow: hidden;
  min-height: 600px;
}
.ulFrame{
  margin-left: -24px;
  float: left;
  padding: 0 20px 20px;
  box-sizing: border-box;
  background-color: white;
  border-radius: 5px;
}
.item{
  margin: 24px 0 0 24px;
  float: left;
  width: 310px;
  border-radius: 8px;
  border: 1px solid #d7d7d7;
  box-sizing: border-box;
  background: #fff;
}
</style>
