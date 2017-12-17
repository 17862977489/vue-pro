<template>
  <div class="layout">
  	<header class="header">
  	  <div class="back iconfont">&#xe648;</div>
  	  <div class="search"><span class="iconfont">&#xe60b;</span><a href="javascript:;">输入城市/景点/游玩主题</a></div>
  	  <div class="city">北京</div>
  	</header>
	<swiper :options="swiperOption">
	    <swiper-slide v-for="item in swiperInfo" :key="item.id">
	 	  <div class="swiper-img-con">
	      	<img class="swiper-img" :src="item.imgUrl" alt="">
	      </div>
	    </swiper-slide>
	    <div class="swiper-pagination"  slot="pagination"></div>
  	</swiper>
  	
    <swiper :options="iconOption" class="pos">
      <swiper-slide v-for="(pageInfo, index) in pages" :key="index">
        <div class="icon-wrapper">
          <div v-for="item in pageInfo" :key="item.id" class="icon-item">
            <div class="icon-img-con">
              <img class="icon-img" :src="item.imgUrl" alt="">
              <div class="icon-title">{{item.title}}</div>
            </div>
          </div>
        </div>
      </swiper-slide>
      <div class="swiper-pagination icon-pagination"  slot="pagination"></div>
    </swiper>
    <div class="link">
      <a href="javascript:;"><i class="iconfont">&#xe600;</i><span>定位失败</span></a>
      <a href="javascript:;" class="br0"><i class="iconfont">&#xe74d;</i><span>5折泡温泉</span></a>
    </div>
    <ul class="ads" >
      <li v-for="item in adsInfo"><a href="javascript:;" :style="item.bgUrl"></a></li>
    </ul>
    <h2 class="recTitle">热销推荐</h2>
    <ul class="recommend">
      <li v-for="item in recommendInfo" class="hotList">
        <a href="javascript:;">
          <div class="hotListImg"><img :src="item.imgUrl"></div>
          <div class="hotListInfo"><div class="hotListTitle">{{item.title}}</div><div class="hotListCon">{{item.con}}</div></div>
          <div class="hotListPrice">￥<em>{{item.price}}</em><span>起</span></div>
        </a>
      </li>
      <a href="javascript:;" class="checkAll">查看所有产品</a>
    </ul>
    <h2 class="whereGo">周末去哪儿</h2>
    <div>
      <div v-for="item in whereInfo" class="whereList">
        <a href="javascript:;">
          <div class="imgCon">
            <img :src="item.imgUrl">
          </div>
          <div class="whereCon">
            <p class="whereName">{{item.title}}</p>
            <p class="whereDes">{{item.con}}</p>
          </div>
        </a>
      </div>
    </div>
    <div class="care">
      <span class="careCon">票面价是指通过景区指定窗口售卖的纸质门票上标注的价格</span>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Index',
    data () {
      return {
        swiperInfo: [],
        iconInfo: [],
        adsInfo: [],
        recommendInfo: [],
        whereInfo: [],
        swiperOption: {
          autoplay: 2000,
          loop: true,
          pagination: '.swiper-pagination'
        },
        iconOption: {
          pagination: '.icon-pagination'
        }
      }
    },
    computed: {
      pages () {
        const pages = []
        this.iconInfo.forEach((value, index) => {
          let page = Math.floor(index / 8)
          if (!pages[page]) {
            pages[page] = []
          }
          pages[page].push(value)
        })
        return pages
      }
    },
    methods: {

      getIndexData () {
        this.$http.get('/static/index.json').then(this.handleGetDataSucc.bind(this))
      },

      handleGetDataSucc (res) {
        const body = res.body
        if (body && body.data && body.data.swiper) {
          this.swiperInfo = body.data.swiper
          this.iconInfo = body.data.icons
          this.adsInfo = body.data.ads
          this.recommendInfo = body.data.recommend
          this.whereInfo = body.data.whereGo
        }
      }
    },

    created () {
      this.getIndexData()
    }
  }
</script>

<style scoped>
  .layout{
    background: #f5f5f5;
  }
  .header {
    display: flex;
    background: #05bad5;
    color:#fff;
  }
  .back{
	width: .64rem;
	line-height: .86rem;
	text-align: center;
	font-size: .38rem;
  }
  .search{
	flex:1;
	margin: .14rem .18rem;
	background: #fff;
	border-radius: .1rem;
  }
  .city{
	width:1.14rem;
	line-height: .86rem;
	text-align:center;
  }
  .swiper-img-con{
    overflow: hidden;
    width: 100%;
    height: 0;
    padding-bottom: 31.25%;
  }
  .swiper-img{
  	width: 100%;
  }
  .icon-item{
    box-sizing: border-box;
    float: left;
    width:25%;
    padding: 0.4rem 0.25rem 0;
  }
  .icon-img-con{
    width: 100%;
    height: 0;
    padding-bottom: 100%;
  }
  .icon-img{
    width: 48%;
    margin-left: 26%;
  }
  .icon-title{
    margin-top: 0.2rem;
    text-align: center;
  }
  .pos{
    position: relative;
    height: 4.2rem;
    background: #fff;
  }
  .icon-pagination{
    position: absolute;
    bottom: 0.16rem;
  }
  .link{
    height: 0.98rem;
    border-top: 1px solid #dadada;
    color: #313131;
    background: #fff;
    margin-bottom: 0.2rem;
  }
  .link a{
    display: block;
    float: left;
    width: 49%;
    text-align: center;
    line-height: 0.98rem;
    font-size: 0.28rem;
    height: 100%;
    border-right: 1px solid #dadada;
  }
  .link .br0{
    border-right: 0;
  }
  .link i{
    color: #616161;
    font-size: 0.32rem;
  }
  .link span{
    color: #313131;
  }
  .ads{
    height: 1.38rem;
    background: #fff;
    width: 100%;
    border-top: 1px solid #dbdbdb;
    border-bottom: 1px solid #dbdbdb;
  }
  .ads li{
    float: left;
    width: 49%;
    height: 100%;
  }
  .ads li a{
    color: #fa3d39;
    display: block;
    height: 100%;
  }
  .recTitle{
    height: 0.8rem;
    padding-left: 0.26rem;
    line-height: 0.8rem;
    color: #212121;
  }
  .hotList{
    position: relative;
    overflow: hidden;
    height: 1.4rem;
    padding: 0.24rem;
    background: #fff;
  }
  .hotListImg{
    position: absolute;
    top: 0.24rem;
    left: 0.24rem;
    width: 1.4rem;
    height: 1.4rem;
  }
  .hotListImg img{
    width: 100%;
    height: 100%;
  }
  .hotListInfo{
    margin-left: 1.6rem;
  }
  .hotListTitle{
    margin-top: 0.04rem;
    margin-bottom: 0.1rem;
    color: #212121;
    font-size: 0.3rem;
  }
  .hotListCon{
    overflow: hidden;
    margin-bottom: 0.1rem;
    height: 0.4rem;
    line-height: 0.4rem;
    color: #9e9e9e;
    white-space: nowrap;
    text-overflow: ellipsis;
  }
  .hotListPrice{
    margin-left: 1.6rem;
    color: #ff8300;
  }
  .hotListPrice em{
    font-size: 0.36rem;
    padding: 0 0.04rem;
  }
  .hotListPrice span{
    color: #9e9e9e;
    font-size: 0.24rem;
  }
  .checkAll{
    display: block;
    width: 100%;
    height: 0.88rem;
    color: #00afc7;
    line-height: 0.88rem;
    text-align: center;
    background: #fff;
  }
  .whereGo{
    color: #212121;
    height: 0.8rem;
    padding-left: 0.26rem;
    line-height: 0.8rem;
    color: #212121;
  }
  .whereList{
    position: relative;
    margin-bottom: 0.1rem;
    background: #fff;
  }
  .imgCon{
    overflow: hidden;
    height: 0;
    padding-bottom: 37.5%;
  }
  .imgCon img{
    width: 100%;
  }
  .whereCon{
    position: relative;
    padding: 0.14rem 0.2rem 0.2rem 0.2rem;
  }
  .whereName{
    overflow: hidden;
    padding-right: 1.4rem;
    color: #212121;
    font-size: 0.28rem;
    line-height: 0.48rem;
    white-space: nowrap;
    text-overflow: ellipsis;
  }
  .whereDes{
    overflow: hidden;
    padding-right: 1.4rem;
    color: #616161;
    font-size: 0.24rem;
    line-height: 0.42rem;
    white-space: nowrap;
    text-overflow: ellipsis;
  }
  .care{
    margin-top: 0.1rem;
    padding: 0.14rem 0.1rem;
    font-size: 0.24rem;
    line-height: 0.32rem;
    background: #fff;
    color: #616161;
  }
  .careCon{
    margin-left: 0.3rem;
  }
</style>