<template>
  <div class="layout-columns-aside">
    <el-scrollbar>
      <ul>
        <li v-for="(v,k) in columnsAsideList" :key="k" @click="onColumnsAsideMenuClick(v,k)"
          :ref="el => { if (el) columnsAsideOffsetTopRefs[k] = el }" :class="{'layout-columns-active':liIndex === k}"
          :title="v.meta.title">
          <div class="layout-columns-aside-li-box" v-if="!v.meta.isLink || v.meta.isLink && v.meta.isIframe">
            <i :class="v.meta.icon"></i>
            <div class="layout-columns-aside-li-box-title font12">
              {{v.meta.title && v.meta.title.length >= 4 ? v.meta.title.substr(0,4) : v.meta.title}}
            </div>
          </div>
          <div class="layout-columns-aside-li-box" v-else>
            <a :href="v.meta.isLink" target="_blank">
              <i :class="v.meta.icon"></i>
              <div class="layout-columns-aside-li-box-title font12">
                {{v.meta.title && v.meta.title.length >= 4 ? v.meta.title.substr(0,4) : v.meta.title}}
              </div>
            </a>
          </div>
        </li>
        <div ref="columnsAsideActiveRef" :class="setColumnsAsideStyle"></div>
      </ul>
    </el-scrollbar>
  </div>
</template>

<script lang="ts">
import {
  reactive,
  toRefs,
  ref,
  computed,
  onMounted,
  nextTick,
  getCurrentInstance,
  watch,
} from "vue";
import { useRoute, useRouter, onBeforeRouteUpdate } from "vue-router";
import { useStore } from "/@/store/index.ts";
export default {
  name: "layoutColumnsAside",
  setup() {
    const columnsAsideOffsetTopRefs = ref([]);
    const columnsAsideActiveRef = ref();
    const { proxy } = getCurrentInstance();
    const store = useStore();
    const route = useRoute();
    const router = useRouter();
    const state = reactive({
      columnsAsideList: [],
      liIndex: 0,
      difference: 0,
      routeSplit: [],
    });
    // 设置高亮样式
    const setColumnsAsideStyle = computed(() => {
      let { columnsAsideStyle } = store.state.themeConfig;
      columnsAsideStyle === "columnsRound"
        ? (state.difference = 3)
        : (state.difference = 0);
      if (columnsAsideStyle === "columnsRound")
        return "layout-columns-round-active";
      else if (columnsAsideStyle === "columnsCard")
        return "layout-columns-card-active";
    });
    // 设置菜单高亮位置移动
    const setColumnsAsideMove = (k: number) => {
      state.liIndex = k;
      columnsAsideActiveRef.value.style.top = `${
        columnsAsideOffsetTopRefs.value[k].offsetTop + state.difference
      }px`;
    };
    // 菜单高亮点击事件
    const onColumnsAsideMenuClick = (v: Object, k: number) => {
      setColumnsAsideMove(k);
      let { path, redirect } = v;
      if (redirect) router.push(redirect);
      else router.push(path);
    };
    // 设置高亮动态位置
    const onColumnsAsideDown = (k: number) => {
      nextTick(() => {
        setColumnsAsideMove(k);
      });
    };
    // 设置/过滤路由（非静态路由/是否显示在菜单中）
    const setFilterRoutes = () => {
      state.columnsAsideList = filterRoutesFun(store.state.routes);
      const resData = setSendChildren(route.path);
      onColumnsAsideDown(resData.item[0].k);
      proxy.mittBus.emit("setSendColumnsChildren", resData);
    };
    // 传送当前子级数据到菜单中
    const setSendChildren = (path: string) => {
      const currentPathSplit = path.split("/");
      let currentData: object = {};
      state.columnsAsideList.map((v, k) => {
        if (v.path === `/${currentPathSplit[1]}`) {
          v["k"] = k;
          currentData["item"] = [{ ...v }];
          currentData["children"] = [{ ...v }];
          if (v.children) currentData["children"] = v.children;
        }
      });
      return currentData;
    };
    // 路由过滤递归函数
    const filterRoutesFun = (arr: Array<object>) => {
      return arr
        .filter((item) => !item.meta.isHide)
        .map((item) => {
          item = Object.assign({}, item);
          if (item.children) item.children = filterRoutesFun(item.children);
          return item;
        });
    };
    // tagsView 点击时，根据路由查找下标 columnsAsideList，实现左侧菜单高亮
    const setColumnsMenuHighlight = (path) => {
      state.routeSplit = path.split("/");
      state.routeSplit.shift();
      const routeFirst = `/${state.routeSplit[0]}`;
      const currentSplitRoute = state.columnsAsideList.find(
        (v) => v.path === routeFirst
      );
      // 延迟拿值，防止取不到
      setTimeout(() => {
        onColumnsAsideDown(currentSplitRoute.k);
      }, 0);
    };
    // 监听路由的变化，动态赋值给菜单中
    watch(store.state, (val) => {
      if (val.routes.length === state.columnsAsideList.length) return false;
      setFilterRoutes();
    });
    // 页面加载时
    onMounted(() => {
      setFilterRoutes();
    });
    // 路由更新时
    onBeforeRouteUpdate((to) => {
      setColumnsMenuHighlight(to.path);
      proxy.mittBus.emit("setSendColumnsChildren", setSendChildren(to.path));
    });
    return {
      columnsAsideOffsetTopRefs,
      columnsAsideActiveRef,
      onColumnsAsideDown,
      setColumnsAsideStyle,
      onColumnsAsideMenuClick,
      ...toRefs(state),
    };
  },
};
</script>

<style scoped lang="scss">
.layout-columns-aside {
  width: 64px;
  height: 100%;
  background: var(--bg-columnsMenuBar);
  ul {
    position: relative;
    li {
      color: var(--bg-columnsMenuBarColor);
      width: 100%;
      height: 50px;
      text-align: center;
      display: flex;
      cursor: pointer;
      position: relative;
      z-index: 1;
      .layout-columns-aside-li-box {
        margin: auto;
        .layout-columns-aside-li-box-title {
          padding-top: 1px;
        }
      }
      a {
        text-decoration: none;
        color: var(--bg-columnsMenuBarColor);
      }
    }
    .layout-columns-active {
      color: #ffffff;
      transition: 0.3s ease-in-out;
    }
    .layout-columns-round-active {
      background: var(--color-primary);
      color: #ffffff;
      position: absolute;
      left: 50%;
      top: 2px;
      height: 44px;
      width: 58px;
      transform: translateX(-50%);
      z-index: 0;
      transition: 0.3s ease-in-out;
      border-radius: 5px;
    }
    .layout-columns-card-active {
      @extend .layout-columns-round-active;
      top: 0;
      height: 50px;
      width: 100%;
      border-radius: 0;
    }
  }
}
</style>