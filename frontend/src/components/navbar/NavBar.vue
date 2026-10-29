<script setup>
import MenuIcon from "@/components/navbar/icons/MenuIcon.vue";
import HomepageIcon from "@/components/navbar/icons/HomepageIcon.vue";
import FriendIcon from "@/components/navbar/icons/FriendIcon.vue";
import CreateIcon from "@/components/navbar/icons/CreateIcon.vue";
import SearchIcon from "@/components/navbar/icons/SearchIcon.vue";
</script>

<template>
  <div class="drawer lg:drawer-open">
      <input id="my-drawer-4" type="checkbox" class="drawer-toggle inline" />
      <div class="drawer-content">
        <nav class="navbar w-full bg-base-100 shadow-sm">
          <div class="navbar-start">
            <label for="my-drawer-4" aria-label="open sidebar" class="btn btn-square btn-ghost drawer-button">
             <MenuIcon/>
            </label>
          <div class="px-2 font-bold text-xl brand-title">AIFriends</div>
          </div>
          <div class="navbar-center w-8/9 max-w-180">
            <div class="join w-5/6 search-group">
              <input class="input join-item rounded-l-full w-5/6" placeholder="搜索你感兴趣的内容" />
              <button class="btn join-item rounded-r-full search-btn"><SearchIcon/>搜索</button>
            </div>
          </div>
          <div class="navbar-end">
            <button class="btn btn-ghost text-lg login-btn">登录</button>
          </div>
        </nav>
        <slot></slot>
      </div>

      <div class="drawer-side is-drawer-close:overflow-visible">
        <label for="my-drawer-4" aria-label="close sidebar" class="drawer-overlay"></label>
        <div class="flex min-h-full flex-col items-start bg-base-200 is-drawer-close:w-16 is-drawer-open:w-54 sidebar-panel">
          <ul class="menu w-full grow">
            <li>
              <button class="is-drawer-close:tooltip is-drawer-close:tooltip-right text-base py-3 nav-item" data-tip="首页">
                <FriendIcon/>
                <span class="is-drawer-close:hidden whitespace-nowrap">首页</span>
              </button>
            </li>
            <li>
              <button class="is-drawer-close:tooltip is-drawer-close:tooltip-right text-base py-3 nav-item" data-tip="好友">
                <HomepageIcon/>
                <span class="is-drawer-close:hidden whitespace-nowrap">好友</span>
              </button>
            </li>
            <li>
              <button class="is-drawer-close:tooltip is-drawer-close:tooltip-right text-base py-3 nav-item" data-tip="创作">
                <CreateIcon/>
                <span class="is-drawer-close:hidden whitespace-nowrap">创作</span>
              </button>
            </li>
          </ul>
        </div>
      </div>
    </div>
</template>

<style scoped>
/* ========== 主题变量（带 fallback，兼容 DaisyUI 5 / 4） ========== */
.drawer {
  --nb-surface: var(--color-base-100, #ffffff);
  --nb-ink: var(--color-base-content, #1f2937);
  --nb-brand: var(--color-primary, #6366f1);
  --nb-brand-2: var(--color-accent, #06b6d4);
  --nb-on-brand: var(--color-primary-content, #ffffff);
}

/* ========== 顶部导航：磨砂玻璃 + 细描边 + 柔和投影 ========== */
/* 仅覆盖 background / box-shadow，宽高与定位完全不受影响 */
.navbar {
  background: color-mix(in oklab, var(--nb-surface) 82%, transparent);
  backdrop-filter: saturate(180%) blur(14px);
  -webkit-backdrop-filter: saturate(180%) blur(14px);
  box-shadow:
    0 1px 0 color-mix(in oklab, var(--nb-ink) 8%, transparent),
    0 10px 28px -20px color-mix(in oklab, var(--nb-ink) 70%, transparent);
}

/* 品牌名：渐变文字（不改变字号与行高） */
.brand-title {
  letter-spacing: 0.02em;
  background-image: linear-gradient(105deg, var(--nb-brand), var(--nb-brand-2));
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  -webkit-text-fill-color: transparent;
}

/* ========== 汉堡按钮 ========== */
.drawer-button {
  transition: background-color 0.2s ease, color 0.2s ease;
}
.drawer-button :deep(svg) {
  transition: transform 0.25s ease;
}
@media (hover: hover) {
  .drawer-button:hover {
    background-color: color-mix(in oklab, var(--nb-brand) 12%, transparent);
    color: var(--nb-brand);
  }
  .drawer-button:hover :deep(svg) {
    transform: scale(1.1);
  }
}

/* ========== 搜索框 ========== */
.search-group .input {
  background-color: color-mix(in oklab, var(--nb-ink) 5%, transparent);
  border-color: transparent;
  transition: background-color 0.2s ease, box-shadow 0.2s ease;
}
.search-group .input::placeholder {
  color: color-mix(in oklab, var(--nb-ink) 45%, transparent);
}
.search-group .input:focus {
  background-color: var(--nb-surface);
  outline: none;
  box-shadow: 0 0 0 3px color-mix(in oklab, var(--nb-brand) 22%, transparent);
}

/* ========== 搜索按钮：品牌渐变 ========== */
.search-btn {
  background-image: linear-gradient(
    120deg,
    var(--nb-brand),
    color-mix(in oklab, var(--nb-brand) 45%, var(--nb-brand-2))
  );
  color: var(--nb-on-brand);
  border-color: transparent;
  box-shadow: 0 2px 10px -6px color-mix(in oklab, var(--nb-brand) 80%, transparent);
  transition: filter 0.2s ease, box-shadow 0.2s ease, transform 0.15s ease;
}
@media (hover: hover) {
  .search-btn:hover {
    filter: brightness(1.07);
    box-shadow: 0 8px 18px -10px color-mix(in oklab, var(--nb-brand) 85%, transparent);
  }
}
.search-btn:active {
  transform: scale(0.98);
}

/* ========== 登录按钮 ========== */
.login-btn {
  transition: background-color 0.2s ease, color 0.2s ease;
}
@media (hover: hover) {
  .login-btn:hover {
    background-color: color-mix(in oklab, var(--nb-brand) 10%, transparent);
    color: var(--nb-brand);
  }
}

/* ========== 侧边栏面板 ========== */
.sidebar-panel {
  /* 叠加在 bg-base-200 上的低透明度渐变，亮/暗主题都自然 */
  background-image: linear-gradient(
    180deg,
    color-mix(in oklab, var(--nb-ink) 2%, transparent),
    color-mix(in oklab, var(--nb-ink) 8%, transparent)
  );
  border-right: 1px solid color-mix(in oklab, var(--nb-ink) 7%, transparent);
  /* 展开/收起时宽度平滑过渡，最终宽度仍由 is-drawer-close/open 决定 */
  transition: width 0.25s ease;
}

/* ========== 侧边栏菜单项 ========== */
.nav-item {
  position: relative; /* 仅供伪元素定位，不参与布局 */
  color: color-mix(in oklab, var(--nb-ink) 75%, transparent);
  transition: background-color 0.2s ease, color 0.2s ease;
}
.nav-item :deep(svg) {
  transition: transform 0.2s ease;
}

@media (hover: hover) {
  .nav-item:hover {
    background-color: color-mix(in oklab, var(--nb-brand) 10%, transparent);
    color: var(--nb-brand);
  }
  .nav-item:hover :deep(svg) {
    transform: scale(1.08);
  }
}

/* 左侧指示条：仅在 lg 常驻展开时出现，收起态保持干净 */
@media (min-width: 1024px) {
  .nav-item::before {
    content: "";
    position: absolute;
    left: 0;
    top: 50%;
    width: 3px;
    height: 0;
    border-radius: 0 3px 3px 0;
    background: var(--nb-brand);
    transform: translateY(-50%);
    transition: height 0.2s ease;
  }
  .nav-item:hover::before {
    height: 50%;
  }
}

/* ========== 抽屉遮罩：轻微模糊背景 ========== */
.drawer-overlay {
  backdrop-filter: blur(2px);
  -webkit-backdrop-filter: blur(2px);
}
</style>