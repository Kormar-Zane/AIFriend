<script setup>
import NavBar from "@/components/navbar/NavBar.vue";
import HomepageIcon from "@/components/navbar/icons/HomepageIcon.vue";
import FriendIcon from "@/components/navbar/icons/FriendIcon.vue";
import CreateIcon from "@/components/navbar/icons/CreateIcon.vue";
import MenuIcon from "@/components/navbar/icons/MenuIcon.vue";
import FriendIndex from "@/views/friend/FriendIndex.vue";
import HomepageIndex from "@/views/homepage/HomepageIndex.vue";
import CreateIndex from "@/views/create/CreateIndex.vue";
import SearchIcon from "@/components/navbar/icons/SearchIcon.vue";
</script>

<template>
  <div class="drawer lg:drawer-open">
    <input id="my-drawer-4" type="checkbox" class="drawer-toggle inline" />
    <div class="drawer-content">
      <!-- Navbar -->
      <nav class="navbar w-full bg-base-300">
        <label for="my-drawer-4" aria-label="open sidebar" class="btn btn-square btn-ghost drawer-button">
          <!-- Sidebar toggle icon -->
          <MenuIcon/>
        </label>
        <div class="px-4 font-bold text-xl brand-title" >AIFriends</div>
        <div class="navbar-center w-4/5 max-w-180 flex justify-center">
        <div class="join w-4/5 flex justify-center">
          <input class="input join-item rounded-l-full w-4/5" placeholder="搜索你感兴趣的内容" />
          <button class="btn join-item rounded-r-full gap-0">
            <SearchIcon/>
            搜索
          </button>
        </div>
        </div>
        <div class="navbar-end">
            <RouterLink :to="{name: 'user-account-login-index'}" class="btn btn-ghost text-lg login-btn">
              登录
            </RouterLink>
        </div>
      </nav>
      <!-- Page content here -->
      <slot></slot>
    </div>

    <div class="drawer-side is-drawer-close:overflow-visible">
      <label for="my-drawer-4" aria-label="close sidebar" class="drawer-overlay"></label>
      <div class="flex min-h-full flex-col items-start bg-base-200 is-drawer-close:w-14 is-drawer-open:w-64">
        <!-- Sidebar content here -->
        <ul class="menu w-full grow">
          <li>
            <!-- HomePage  -->
            <RouterLink :to="{name: 'homepage-index'}" class="is-drawer-close:tooltip is-drawer-close:tooltip-right" data-tip="首页">
              <HomepageIcon/>
              <span class="is-drawer-close:hidden">首页</span>
            </RouterLink>
          </li>

          <li>
            <!-- Friend -->
            <RouterLink :to="{name: 'friend-index'}" class="is-drawer-close:tooltip is-drawer-close:tooltip-right" data-tip="好友">
              <FriendIcon/>
              <span class="is-drawer-close:hidden">好友</span>
            </RouterLink>
          </li>

          <li>
            <!-- Create -->
            <RouterLink :to="{name: 'create-index'}" class="is-drawer-close:tooltip is-drawer-close:tooltip-right" data-tip="创作">
              <CreateIcon/>
              <span class="is-drawer-close:hidden">创作</span>
            </RouterLink>
          </li>
        </ul>
      </div>
    </div>
  </div>
  <NavBar></NavBar>
</template>

<style scoped>
/* ① 选中色变浅（沿用上一版） */
.menu :deep(.router-link-active),
.menu :deep(.router-link-exact-active),
.menu :deep(.active),
.menu :deep(.menu-active) {
  background-color: var(--color-base-300);
  color: var(--color-base-content);
}

/* ② 阴影减弱：去掉菜单项默认的 box-shadow / 焦点环 */
.menu :deep(li > a),
.menu :deep(li > button) {
  box-shadow: none;
}

.menu :deep(li > a:focus-visible),
.menu :deep(li > button:focus-visible) {
  box-shadow: none;
  outline: none;          /* 不想去掉键盘焦点环的话，这行可删 */
}

/* ③ 收起抽屉时悬停出现的小 tooltip 也顺手减淡阴影 */
.menu :deep(.tooltip::before) {
  box-shadow: 0 1px 2px rgb(0 0 0 / 0.06);
}
</style>