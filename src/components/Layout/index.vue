<template>
  <el-menu
    :default-active="activeIndex"
    :router="true"
    mode="horizontal"
    background-color="#222832"
    text-color="#cfd3dc"
    active-text-color="#ffffff"
    class="top-menu"
  >
    <template v-for="item in menus" :key="item.index">
      <el-sub-menu v-if="item.subs" :index="item.index">
        <template #title>{{ item.title }}</template>
        <el-menu-item v-for="sub in item.subs" :key="sub.index" :index="sub.index">
          {{ sub.title }}
        </el-menu-item>
      </el-sub-menu>
      <el-menu-item v-else :index="item.index">{{ item.title }}</el-menu-item>
    </template>
  </el-menu>
</template>

<script lang="ts" setup>
  import { computed } from 'vue'
  import { useRoute } from 'vue-router'

  type MenuItem = { index: string; title: string; subs?: MenuItem[] }

  // 菜单项与路由保持同步
  const menus: MenuItem[] = [
    { index: '/home', title: '系统首页' },
    { index: '/curvedata', title: '曲线数据' },
    {
      index: '/user',
      title: '用户管理',
      subs: [
        { index: '/userList', title: '用户列表' },
        { index: '/addUser', title: '新增用户' },
      ],
    },
  ]

  const route = useRoute()
  const activeIndex = computed(() => route.path)
</script>

<style scoped lang="less">
  .top-menu {
    flex: 1;
    height: 60px;
    border-bottom: none;
    min-width: 0; // 允许 flex 收缩

    // 水平菜单项高度对齐顶栏
    :deep(.el-menu-item),
    :deep(.el-sub-menu__title) {
      height: 60px;
      line-height: 60px;
    }
  }
</style>
