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
      <div>
        <h1 class="list-title">热门歌单推荐</h1>
      </div>
    </div>
</template>

<script>
  import {getRecommend, getSongList} from "api/recommend";
  import {ERR_OK} from "api/config";
  import Slider from "base/slider/slider";

  export default {
    data() {
      return {
        recommends: []
      }
    },
    created() {
      this._getRecommend()
      this._getSongList()
    },
    methods: {
      _getRecommend() {
        getRecommend().then((res) => {
          if (res.code === ERR_OK) {
            this.recommends = res.data.slider
          }
        })
      },
      _getSongList() {
        getSongList(1).then((resp) => {
          console.log(resp)
        })
      }
    },
    components: {
      Slider
    }
  }
</script>

<style scoped>
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
  .list-title{
    color: yellow;
    text-align: center;
    font: bold 17px/20px '微软雅黑';
  }

</style>
