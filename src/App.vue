<template>
  <div id="app">
    <el-container v-if="showMenu" class="app-container">
      <el-header class="top-bar" height="60px">
        <div class="logo">Secret Garden</div>
        <Layout />
        <TopHeader />
      </el-header>
      <el-main class="main-content">
        <router-view />
      </el-main>
    </el-container>
    <router-view v-else />
  </div>
</template>
<script lang="ts">
  import Layout from '/@/components/Layout/index.vue'
  import TopHeader from '/@/components/Header/index.vue'

  export default {
    components: {
      Layout,
      TopHeader,
    },
    setup() {
      const state = reactive({
        showMenu: true,
      })

      const route = useRoute()
      watch(
        () => route.path,
        () => {
          state.showMenu = !route.path.includes('login')
        },
      )

      return {
        ...toRefs(state),
      }
    },
  }
</script>

<style scoped lang="less">
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    background-color: var(--color-bg-1);
  }

  .app-container {
    height: 100vh;
  }

  .top-bar {
    display: flex;
    align-items: center;
    background-color: #222832;
    padding: 0 20px;
    box-shadow: 0 1px 4px rgba(0, 0, 0, 0.08);
    z-index: 10;

    .logo {
      flex-shrink: 0;
      width: 160px;
      color: #fff;
      font-weight: 600;
      font-size: 18px;
      letter-spacing: 1px;
    }
  }

  .main-content {
    background-color: #f5f7fa;
    padding: 20px;
  }
</style>
