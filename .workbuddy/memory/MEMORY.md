# admin-pj 项目记忆

## 项目概况

- 基于 fast-vue3 模板脚手架：Vue3 + Vite2 + TypeScript + Pinia + Element Plus + WindiCSS
- Hash 路由 (createWebHashHistory)
- pnpm 管理依赖

## 登录认证体系

- 登录页面: src/pages/login/index.vue (username + password 表单)
- API: src/api/user/index.ts (POST /user/login, GET /user/profile, POST /user/logout)
- Store: src/store/modules/user/index.ts (Pinia, login/logout/getInfo actions)
- Token 管理: src/utils/auth.ts (localStorage key='fast-token', value='Bearer xxx')
- 路由守卫: src/router/index.ts (beforeEach, isLogin() 检查 token)
- HTTP 封装: src/utils/http/axios/index.ts (统一响应 IResponse{code,result,message})

## 认证流程简述

1. 路由守卫 beforeEach → isLogin() → 无 token 跳转/login
2. 登录页 clearToken() → 表单提交 → userStore.login() → POST /user/login
3. 返回 {token} → setToken(Bearer+token) → localStorage → router.push('/home')
4. 首页 Header 调用 userStore.getInfo() → GET /user/profile → 显示用户信息
5. 退出: userStore.logout() → POST /user/logout + resetInfo + clearToken + location.reload

## 注意事项

- 无验证码/记住密码/SSO/角色权限
- token 存 localStorage 持久化
- axios defaults.headers.authorization 只在模块加载时读取一次
- 退出用 location.reload() 强制刷新
