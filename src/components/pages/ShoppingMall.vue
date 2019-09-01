<template>
  <div>
    <div class="search-bar">
      <van-row>
        <van-col span="3">
          <img :src="locationIcon" width="80%" class="location-icon" />
        </van-col>
        <van-col span="15">
          <input type="text" class="search-input" />
        </van-col>
        <van-col span="6">
          <van-button type="mini">查找</van-button>
        </van-col>
      </van-row>
    </div>
    <div class="swipe-area">
      <van-swipe :autoplay="3000">
        <van-swipe-item v-for="(pic,index) in swipePicArr" :key="index">
          <img v-lazy="pic.image"  width="100%" />
        </van-swipe-item>
      </van-swipe>
    </div>
    <!-- type bar -->
    <div class="type-bar">
      <div v-for="(cate,index) in category" :key="index">
        <img v-lazy="cate.image" width="90%" />
        <span>{{cate.mallCategoryName}}</span>
      </div>
    </div>
    <!--adBanner bar -->

      <div class="adBanner">
         <img v-lazy="advertesPicture" width="100%">
      </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      locationIcon: require("../../assets/images/dingwei.png"),
      category: [],
      advertesPicture:'',
      swipePicArr: []
    };
  },
  created() {
    axios({
      url:
        "https://www.easy-mock.com/mock/5d6bd43e3efa773f8b0bf825/smileshop/index",
      method: "get"
    })
      .then(res => {
        if (res.status === 200) {
          console.log(res.data)
          this.category = res.data.data.category;
          this.advertesPicture= res.data.data.advertesPicture.PICTURE_ADDRESS;
          this.swipePicArr=res.data.data.slides;
        }
      })
      .catch(err => {
        console.log(err);
      });
  }
};
</script>

<style scoped>
.search-bar {
  height: 2.2rem;
  background-color: #e5017d;
  line-height: 2.2rem;
  overflow: hidden;
}
.search-input {
  width: 100%;
  height: 1.3rem;
  border-top: 0px;
  border-left: 0px;
  border-right: 0px;
  border-bottom: 1px solid #fff !important;
  background-color: #e5017d;
  color: #fff;
}
.location-icon {
  padding-top: 0.2rem;
  padding-left: 0.3rem;
}
.swipe-area {
  max-height: 15rem;
  clear: both;
  overflow: hidden;
}

.type-bar {
  background-color: #fff;
  margin: 0 0.3rem 0.3rem 0.3rem;
  border-radius: 0.3rem;
  font-size: 14px;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
}
.type-bar div {
  padding: 0.3rem;
  font-size: 12px;
  text-align: center;
  flex: 1;
}
</style>
