<template>
  <div id="app">
    <c-header></c-header>
    <tab></tab>
    <keep-alive>
      <router-view/>
    </keep-alive>
  </div>
</template>

<script>
  import CHeader from 'components/c-header/c-header'
  import Tab from 'components/tab/tab'
export default {
  name: 'App',
  components: {
    CHeader,
    Tab
  }
}
</script>

<style>
  body{
    background: #222;
    margin: 0;
    padding: 0;
  }
#app {

  padding: 0;
  margin: 0;
}
</style>
