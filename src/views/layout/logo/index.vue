<template>
  <div class="layout-logo" v-if="setShowLogo" @click="onThemeConfigChange">
    <img src="https://gitee.com/lyt-top/vue-next-admin-images/raw/master/logo/logo-mini.svg"
      class="layout-logo-medium-img" />
    <span>{{config.globalTitle}}</span>
  </div>
  <div class="layout-logo-size" v-else @click="onThemeConfigChange">
    <img src="https://gitee.com/lyt-top/vue-next-admin-images/raw/master/logo/logo-mini.svg"
      class="layout-logo-size-img" />
  </div>
</template>

<script lang="ts">
import { reactive, toRefs, computed, getCurrentInstance } from "vue";
import { useStore } from "/@/store/index.ts";
import config from "/@/utils/themeConfig.ts";
export default {
  name: "layoutLogo",
  setup() {
    const { proxy } = getCurrentInstance();
    const store = useStore();
    const state = reactive({
      config,
    });
    // 设置 logo 的显示。classic 经典布局默认显示 logo
    const setShowLogo = computed(() => {
      let { isCollapse, layout } = store.state.themeConfig;
      return (
        !isCollapse || layout === "classic" || document.body.clientWidth < 1000
      );
    });
    // logo 点击实现菜单展开/收起
    const onThemeConfigChange = () => {
      if (store.state.themeConfig.layout === "transverse") return false;
      proxy.mittBus.emit("onMenuClick");
      store.state.themeConfig.isCollapse = !store.state.themeConfig.isCollapse;
    };
    return {
      setShowLogo,
      onThemeConfigChange,
      ...toRefs(state),
    };
  },
};
</script>

<style scoped lang="scss">
.layout-logo {
  width: 220px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: rgb(0 21 41 / 2%) 0px 1px 4px;
  color: var(--color-primary);
  font-size: 16px;
  cursor: pointer;
  animation: logoAnimation 0.3s ease-in-out;
  &:hover {
    span {
      color: var(--color-primary-light-2);
    }
  }
  &-medium-img {
    width: 20px;
    margin-right: 5px;
  }
}
.layout-logo-size {
  width: 100%;
  height: 50px;
  display: flex;
  cursor: pointer;
  animation: logoAnimation 0.3s ease-in-out;
  &-img {
    width: 20px;
    margin: auto;
  }
  &:hover {
    img {
      animation: logoAnimation 0.3s ease-in-out;
    }
  }
}
</style>