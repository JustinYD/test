<template>
  <div id="app">
    <router-view />
    <van-tabbar route>
      <van-tabbar-item replace to="/home" icon="home-o">首页</van-tabbar-item>
      <van-tabbar-item replace to="/about" icon="setting-o">设置</van-tabbar-item>
    </van-tabbar>
  </div>
</template>

<style>
</style>
