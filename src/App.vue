<template>
  <div id="app" class="fillcontain">
    <el-container>
      <el-header class="header">
        <vheader/>
      </el-header>
      <el-container>
        <el-aside width="10%">
          <navmenu></navmenu>
        </el-aside>
        <el-main width="90%"><router-view></router-view></el-main>
      </el-container>
    </el-container>

  </div>
</template>

<script>
  import NavMenu from '@/components/NavMenu'
  import Header from '@/components/Header'

  export default {
    name: 'App',
    components: {
      'navmenu': NavMenu,
      'vheader': Header
    }
  }
</script>

<style lang="less">
  @import './style/common';
  .header {
    background-color: #409EFF;
    color: #fff;
    line-height: 60px;
  }
</style>
