<template>
  <el-main class="layout-main">
    <el-scrollbar class="layout-scrollbar" ref="layoutScrollbarRef"
      v-show="!currentRouteMeta.isLink && !currentRouteMeta.isIframe"
      :style="{minHeight: `calc(100vh - ${headerHeight}`}">
      <LayoutParentView />
      <Footer v-if="getThemeConfig.isFooter" />
    </el-scrollbar>
    <Link :style="{height: `calc(100vh - ${headerHeight}`}" :meta="currentRouteMeta"
      v-if="currentRouteMeta.isLink && !currentRouteMeta.isIframe" />
    <Iframes :style="{height: `calc(100vh - ${headerHeight}`}" :meta="currentRouteMeta"
      v-if="currentRouteMeta.isLink && currentRouteMeta.isIframe" />
  </el-main>
</template>

<script lang="ts">
import {
  computed,
  defineComponent,
  toRefs,
  reactive,
  getCurrentInstance,
  watch,
  onBeforeMount,
} from "vue";
import { useRoute } from "vue-router";
import { useStore } from "/@/store/index.ts";
import LayoutParentView from "/@/views/layout/routerView/parent.vue";
import Footer from "/@/views/layout/footer/index.vue";
import Link from "/@/views/layout/routerView/link.vue";
import Iframes from "/@/views/layout/routerView/iframes.vue";
export default defineComponent({
  name: "layoutMain",
  components: { LayoutParentView, Footer, Link, Iframes },
  setup() {
    const { proxy } = getCurrentInstance();
    const store = useStore();
    const route = useRoute();
    const state = reactive({
      headerHeight: "",
      currentRouteMeta: {},
    });
    // 获取布局配置信息
    const getThemeConfig = computed(() => {
      return store.state.themeConfig;
    });
    // 初始化当前路由 meta 信息
    const initCurrentRouteMeta = (meta: object) => {
      state.currentRouteMeta = meta;
    };
    // 设置 main 的高度
    const initHeaderHeight = () => {
      let { isTagsview } = store.state.themeConfig;
      if (isTagsview) return (state.headerHeight = `84px`);
      else return (state.headerHeight = `50px`);
    };
    // 页面加载前
    onBeforeMount(() => {
      initCurrentRouteMeta(route.meta);
      initHeaderHeight();
    });
    // 监听 themeConfig 配置文件的变化，更新菜单 el-scrollbar 的高度
    watch(store.state.themeConfig, (val) => {
      state.headerHeight = val.isTagsview ? "84px" : "50px";
      if (val.isFixedHeaderChange !== val.isFixedHeader) {
        if (!proxy.$refs.layoutScrollbarRef) return false;
        proxy.$refs.layoutScrollbarRef.update();
      }
    });
    // 监听路由的变化
    watch(
      () => route.path,
      () => {
        initCurrentRouteMeta(route.meta);
        proxy.$refs.layoutScrollbarRef.wrap.scrollTop = 0;
      }
    );
    return {
      getThemeConfig,
      initCurrentRouteMeta,
      ...toRefs(state),
    };
  },
});
</script>
