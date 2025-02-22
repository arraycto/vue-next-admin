<template>
  <div class="icon-selector">
    <el-popover :placement="placement" :width="fontIconWidth" v-model:visible="fontIconVisible"
      popper-class="icon-selector-popper">
      <template #reference>
        <el-input v-model="fontIcon" placeholder="请点击选择图标" clearable size="small" ref="inputWidthRef"
          :prefix-icon="fontIconPrefix" @clear="onClearFontIcon"></el-input>
      </template>
      <transition name="el-zoom-in-top">
        <div class="icon-selector-warp" v-show="fontIconVisible">
          <div class="icon-selector-warp-title">请选择一个图标</div>
          <div v-if="isAllOn" class="icon-selector-all">
            <el-input v-model="fontIconSearch" placeholder="请输入内容进行搜索" size="small"></el-input>
            <div class="icon-selector-all-tabs">
              <div class="icon-selector-all-tabs-item" v-for="(v,k) in fontIconTabsList" :key="k"
                @click="onFontIconTabsClick(v,k)" :class="{'icon-selector-all-tabs-active': fontIconTabsIndex === k}">
                <div class="label">{{v.label}}</div>
              </div>
            </div>
          </div>
          <div class="icon-selector-warp-row">
            <el-row :gutter="10">
              <el-col :xs="4" :sm="4" :md="2" :lg="2" :xl="1" :class="`${iconShow}-col`" @click="onColClick(v,k)"
                v-for="(v,k) in fontIconSheetsFilterList" :key="k">
                <div class="icon-selector-warp-item" :class="{'icon-selector-active': fontIconIndex === k}">
                  <div class="flex-margin">
                    <div class="icon-selector-warp-item-value">
                      <i :class="[iconShow,v]"></i>
                    </div>
                  </div>
                </div>
              </el-col>
            </el-row>
            <el-empty :image-size="100" v-if="fontIconSheetsFilterList.length <= 0"></el-empty>
          </div>
        </div>
      </transition>
    </el-popover>
  </div>
</template>

<script lang="ts">
import { ref, toRefs, reactive, onMounted, nextTick, computed } from "vue";
import initIconfont from "/@/utils/getStyleSheets.ts";
import { stat } from "node:fs";
export default {
  name: "iconSelector",
  props: {
    // 是否开启高级功能
    isAllOn: {
      type: Boolean,
      default: () => false,
    },
    // 出现位置
    placement: {
      type: String,
      default: () => "bottom",
    },
  },
  setup(props, { emit }) {
    const inputWidthRef = ref();
    const state = reactive({
      fontIcon: "",
      fontIconPrefix: "",
      fontIconVisible: false,
      fontIconWidth: 0,
      fontIconIndex: "",
      fontIconSearch: "",
      fontIconTabsIndex: 0,
      fontIconTabsList: [
        { label: "iconfont" },
        { label: "element" },
        { label: "awesome" },
      ],
      fontIconSheetsList: [],
      fontIconSheetsListAli: [],
      fontIconSheetsListEle: [],
      fontIconSheetsListAwe: [],
    });
    // 设置 iconShow 的动态显示
    const iconShow = computed(() => {
      if (state.fontIconTabsIndex === 0) return `iconfont ali`;
      else if (state.fontIconTabsIndex === 1) return `ele`;
      else if (state.fontIconTabsIndex === 2) return `fa awe`;
    });
    // 设置无数据时的空状态
    const fontIconSheetsFilterList = computed(() => {
      if (!state.fontIconSearch) return state.fontIconSheetsList;
      let search = state.fontIconSearch.trim().toLowerCase();
      return state.fontIconSheetsList.filter((item) => {
        if (item.toLowerCase().indexOf(search) !== -1) return item;
      });
    });
    // 获取 input 的宽度
    const getInputWidth = () => {
      nextTick(() => {
        state.fontIconWidth = inputWidthRef.value.$el.offsetWidth;
      });
    };
    // 监听页面宽度改变
    const initResize = () => {
      window.addEventListener("resize", () => {
        getInputWidth();
      });
    };
    // 初始化数据
    const initFontIconData = () => {
      initIconfont.ali().then((res) => {
        state.fontIconSheetsList = res;
        state.fontIconSheetsListAli = res;
      });
      initIconfont.ele().then((res) => {
        state.fontIconSheetsListEle = res;
      });
      initIconfont.awe().then((res) => {
        state.fontIconSheetsListAwe = res;
      });
    };
    // 当前项点击
    const onColClick = (v, k) => {
      state.fontIconIndex = k;
      state.fontIcon = v;
      state.fontIconVisible = false;
      if (state.fontIconTabsIndex === 0)
        state.fontIconPrefix = `iconfont ali ${v}`;
      else if (state.fontIconTabsIndex === 1) state.fontIconPrefix = `ele ${v}`;
      else if (state.fontIconTabsIndex === 2)
        state.fontIconPrefix = `fa awe ${v}`;
      emit("get", state.fontIconPrefix);
    };
    // input 点击清除按钮时
    const onClearFontIcon = () => {
      state.fontIconIndex = "";
      state.fontIconPrefix = "";
      emit("get", state.fontIconPrefix);
    };
    // tabs 点击
    const onFontIconTabsClick = (v, k) => {
      state.fontIconTabsIndex = k;
      if (v.label === "iconfont") {
        state.fontIconSheetsList = state.fontIconSheetsListAli;
      } else if (v.label === "element") {
        state.fontIconSheetsList = state.fontIconSheetsListEle;
      } else if (v.label === "awesome") {
        state.fontIconSheetsList = state.fontIconSheetsListAwe;
      }
    };
    // 页面加载时
    onMounted(() => {
      initFontIconData();
      initResize();
      getInputWidth();
    });
    return {
      inputWidthRef,
      iconShow,
      fontIconSheetsFilterList,
      onColClick,
      onClearFontIcon,
      onFontIconTabsClick,
      ...toRefs(state),
    };
  },
};
</script>