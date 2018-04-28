<template>
  <div class="tab">
    <router-link to="recommend">
      推荐
    </router-link>
    <router-link to="singer">
      歌手
    </router-link>
    <router-link to="makeMenu">
      制作菜单
    </router-link>
    <router-link to="vote">
      投票
    </router-link>
  </div>

</template>

<script>
    export default {
        name: "tab"
    }
</script>

<style scoped>
  .tab{
    position: fixed;
    background: #222;
    width: 100%;
    top: 40px;
    left: 0px;
  }
  .tab > a{
    float: left;
    width: 25%;
    text-align: center;
    text-decoration: none;
    color: #efefef;
    font: normal 15px/25px '微软雅黑';
  }
  .tab > a.router-link-active{
    color: yellow;
  }
</style>
