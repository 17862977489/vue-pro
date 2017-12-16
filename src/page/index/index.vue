<template>
  <div>
  	<header class="header">
  	  <div class="back iconfont">&#xe648;</div>
  	  <div class="search"></div>
  	  <div class="city">城市</div>
  	</header>
	<swiper :options="swiperOption" ref="mySwiper">
	    <swiper-slide v-for="item in swiperInfo" :key="item.id">
	 	  <div class="swiper-img-con">
	      	<img class="swiper-img" :src="item.imgUrl" alt="">
	      </div>
	    </swiper-slide>
	    <div class="swiper-pagination"  slot="pagination"></div>
  	</swiper>
  	<div>12131321</div>
  </div>
</template>

<script>
  export default {
    name: 'Index',
    data () {
      return {
        swiperInfo: [],
        swiperOption: {
          autoplay: 2000,
          direction: 'horizontal',
          loop: true,
          pagination: '.swiper-pagination'
        }
      }
    },

    created () {
      this.getIndexData()
    },

    methods: {

      getIndexData () {
        this.$http.get('/static/index.json').then(this.handleGetDataSucc.bind(this))
      },

      handleGetDataSucc (res) {
        this.swiperInfo = res.body.data.swiper
      }
    }
  }
</script>

<style scoped>
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
</style>