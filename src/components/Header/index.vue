<script lang="ts" setup>
  import { storeToRefs } from 'pinia'
  import { useUserStore } from '/@/store'

  const userStore = useUserStore()
  userStore.getInfo()
  const { user_name, avatar } = storeToRefs(userStore)

  const logout = () => userStore.logout()
</script>

<template>
  <div class="header-right">
    <el-popover trigger="hover" :width="120" placement="bottom-end">
      <template #reference>
        <div class="user-con">
          <img v-if="avatar" :src="avatar" class="avatar" />
          <span class="user-name">{{ user_name }}</span>
        </div>
      </template>
      <div class="logout-btn" @click="logout">退出登录</div>
    </el-popover>
  </div>
</template>

<style lang="less" scoped>
  .header-right {
    display: flex;
    align-items: center;
    flex-shrink: 0;
  }

  .user-con {
    display: flex;
    align-items: center;
    cursor: pointer;
    color: #fff;

    .avatar {
      width: 32px;
      height: 32px;
      border-radius: 50%;
      margin-right: 8px;
      object-fit: cover;
    }

    .user-name {
      font-size: 14px;
    }
  }

  .logout-btn {
    text-align: center;
    cursor: pointer;
    padding: 6px 0;
    color: #f56c6c;

    &:hover {
      opacity: 0.8;
    }
  }
</style>
