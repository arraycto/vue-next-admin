<template>
  <div class="layout-scrollbar">
    <div class="layout-view-bg-white flex h100" v-loading="iframeLoading">
      <iframe :src="iframeUrl" frameborder="0" height="100%" width="100%" id="iframe"></iframe>
    </div>
  </div>
</template>

<script lang="ts">
import {
  defineComponent,
  computed,
  reactive,
  toRefs,
  onMounted,
  onBeforeMount,
  onUnmounted,
  nextTick,
  getCurrentInstance,
} from "vue";
import { useRoute } from "vue-router";
export default defineComponent({
  name: "layoutIfameView",
  props: {
    meta: {
      type: Object,
      default: () => {},
    },
  },
  setup(props) {
    const { proxy } = getCurrentInstance();
    const route = useRoute();
    const state = reactive({
      iframeLoading: true,
      iframeUrl: "",
    });
    // 初始化页面加载 loading
    const initIframeLoad = () => {
      nextTick(() => {
        state.iframeLoading = true;
        const iframe = document.getElementById("iframe");
        if (!iframe) return false;
        iframe.onload = () => {
          state.iframeLoading = false;
        };
      });
    };
    // 页面加载前
    onBeforeMount(() => {
      state.iframeUrl = props.meta.isLink;
      proxy.mittBus.on("onTagsViewRefreshRouterView", (path: string) => {
        if (route.path !== path) return false;
        state.iframeUrl = `${props.meta.isLink}?key=${Math.random()}`;
        initIframeLoad();
      });
    });
    // 页面加载时
    onMounted(() => {
      initIframeLoad();
    });
    // 页面卸载时
    onUnmounted(() => {
      proxy.mittBus.off("onTagsViewRefreshRouterView", () => {
        console.log(1111);
      });
    });
    return {
      ...toRefs(state),
    };
  },
});
</script>