<template>
    <div class="recommend">
      <div v-if="recommends.length" class="slider-wrapper" ref="sliderWrapper">
        <slider>
          <div v-for="item in recommends">
            <a :href="item.linkUrl">
              <img class="needsclick" :src="item.picUrl">
            </a>
          </div>
        </slider>
      </div>
      <div class="recommend-list">
        <h1 class="list-title">热门歌单推荐</h1>
        <ul>
          <li v-for="item in discList" class="item">
            <div class="icon">
              <img :src="item.imgurl" width="60" height="60" alt="">
            </div>
            <div class="text">
              <h2 class="name" v-html="item.creator.name"></h2>
              <p class="desc" v-html="item.dissname"></p>
            </div>
          </li>
        </ul>
      </div>
    </div>
</template>

<script>
  import {getRecommend, getDiscList} from "api/recommend";
  import {ERR_OK} from "api/config";
  import Slider from "base/slider/slider";

  export default {
    data() {
      return {
        recommends: [],
        discList: []
      }
    },
    created() {
      this._getRecommend()
      this._getDiscList()
    },
    methods: {
      _getRecommend() {
        getRecommend().then((res) => {
          if (res.code === ERR_OK) {
            this.recommends = res.data.slider
          }
        })
      },
      _getDiscList() {
        getDiscList().then((res) => {
          if (res.code ==- ERR_OK) {
            this.discList = res.data.list
          }
        })
      }
    },
    components: {
      Slider
    }
  }
</script>

<style scoped>
  ul,li{
    padding: 0;
    margin: 0;
  }
  .recommend{
    position: fixed;
    width: 100%;
    top: 88px;
    bottom: 0;
  }
  .recommend-content{
    height: 100%;
    overflow: hidden;
  }
  .slider-wrapper{
    position: relative;
    width: 100%;
    overflow: hidden;
  }
  .recommend-list .list-title{
    color: yellow;
    text-align: center;
    font: bold 17px/20px '微软雅黑';
  }
  .recommend-list .item{
    display: flex;
    box-sizing: border-box;
    align-items: center;
    padding: 0 20px 20px 20px;
  }
  .recommend-list .icon{
    flex: 0 0 60px;
    width: 60px;
    padding-right: 20px;
  }
  .recommend-list .text{
    display: flex;
    flex-direction: column;
    justify-content: center;
    flex: 1;
    line-height: 20px;
    overflow: hidden;
    font-size: 13px
  }
  .recommend-list .name{
    margin-bottom: 10px;
    font-size: 15px;
    color: #fefefe
  }
  .recommend-list .desc{
    color: #ddd
  }


</style>
