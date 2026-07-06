<template>
  <div class="curvedata-wrap">
    <iframe :src="frameSrc" class="curvedata-iframe" frameborder="0" allowfullscreen></iframe>
  </div>
</template>

<script lang="ts" setup>
  // RAWGraphs 项目以 iframe 形式嵌入
  // 本地开发：http://localhost:3000/
  // 生产部署：/rawgraphs/ （admin-pj/public/rawgraphs 构建产物）
  const frameSrc = import.meta.env.MODE === 'development' ? 'http://localhost:8080/' : '/rawgraphs/'
</script>

<style scoped lang="less">
  .curvedata-wrap {
    width: 100%;
    height: calc(100vh - 100px); // 减去 el-header 高度 + el-main padding
    overflow: hidden;

    .curvedata-iframe {
      width: 100%;
      height: 100%;
      border: none;
      display: block;
    }
  }
</style>
