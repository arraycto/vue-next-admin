<template>
  <div class="layout-breadcrumb-seting">
    <el-drawer title="布局配置" v-model="getThemeConfig.isDrawer" direction="rtl" destroy-on-close size="240px"
      @close="onDrawerClose">
      <el-scrollbar class="layout-breadcrumb-seting-bar">
        <!-- 全局主题 -->
        <el-divider content-position="left">全局主题</el-divider>
        <div class="layout-breadcrumb-seting-bar-flex">
          <div class="layout-breadcrumb-seting-bar-flex-label">primary</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-color-picker v-model="getThemeConfig.primary" size="small" @change="onColorPickerChange('primary')">
            </el-color-picker>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex">
          <div class="layout-breadcrumb-seting-bar-flex-label">success</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-color-picker v-model="getThemeConfig.success" size="small" @change="onColorPickerChange('success')">
            </el-color-picker>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex">
          <div class="layout-breadcrumb-seting-bar-flex-label">info</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-color-picker v-model="getThemeConfig.info" size="small" @change="onColorPickerChange('info')">
            </el-color-picker>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex">
          <div class="layout-breadcrumb-seting-bar-flex-label">warning</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-color-picker v-model="getThemeConfig.warning" size="small" @change="onColorPickerChange('warning')">
            </el-color-picker>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex">
          <div class="layout-breadcrumb-seting-bar-flex-label">danger</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-color-picker v-model="getThemeConfig.danger" size="small" @change="onColorPickerChange('danger')">
            </el-color-picker>
          </div>
        </div>

        <!-- 菜单 / 顶栏 -->
        <el-divider content-position="left">菜单 / 顶栏</el-divider>
        <div class="layout-breadcrumb-seting-bar-flex">
          <div class="layout-breadcrumb-seting-bar-flex-label">顶栏背景</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-color-picker v-model="getThemeConfig.topBar" size="small" @change="onBgColorPickerChange('topBar')">
            </el-color-picker>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex">
          <div class="layout-breadcrumb-seting-bar-flex-label">菜单背景</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-color-picker v-model="getThemeConfig.menuBar" size="small" @change="onBgColorPickerChange('menuBar')">
            </el-color-picker>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex">
          <div class="layout-breadcrumb-seting-bar-flex-label">分栏菜单背景</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-color-picker v-model="getThemeConfig.columnsMenuBar" size="small"
              @change="onBgColorPickerChange('columnsMenuBar')">
            </el-color-picker>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex">
          <div class="layout-breadcrumb-seting-bar-flex-label">顶栏默认字体颜色</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-color-picker v-model="getThemeConfig.topBarColor" size="small"
              @change="onBgColorPickerChange('topBarColor')">
            </el-color-picker>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex">
          <div class="layout-breadcrumb-seting-bar-flex-label">菜单默认字体颜色</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-color-picker v-model="getThemeConfig.menuBarColor" size="small"
              @change="onBgColorPickerChange('menuBarColor')">
            </el-color-picker>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex">
          <div class="layout-breadcrumb-seting-bar-flex-label">分栏菜单默认字体颜色</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-color-picker v-model="getThemeConfig.columnsMenuBarColor" size="small"
              @change="onBgColorPickerChange('columnsMenuBarColor')">
            </el-color-picker>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex mt10">
          <div class="layout-breadcrumb-seting-bar-flex-label">顶栏背景渐变</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-switch v-model="getThemeConfig.isTopBarColorGradual" @change="onTopBarGradualChange"></el-switch>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex mt14">
          <div class="layout-breadcrumb-seting-bar-flex-label">菜单背景渐变</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-switch v-model="getThemeConfig.isMenuBarColorGradual" @change="onMenuBarGradualChange"></el-switch>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex mt14">
          <div class="layout-breadcrumb-seting-bar-flex-label">菜单字体背景高亮</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-switch v-model="getThemeConfig.isMenuBarColorHighlight" @change="onMenuBarHighlightChange"></el-switch>
          </div>
        </div>

        <!-- 界面设置 -->
        <el-divider content-position="left">界面设置</el-divider>
        <div class="layout-breadcrumb-seting-bar-flex">
          <div class="layout-breadcrumb-seting-bar-flex-label">菜单水平折叠</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-switch v-model="getThemeConfig.isCollapse" @change="onThemeConfigChange"></el-switch>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex mt15">
          <div class="layout-breadcrumb-seting-bar-flex-label">菜单手风琴</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-switch v-model="getThemeConfig.isUniqueOpened" @change="setLocalThemeConfig"></el-switch>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex mt15">
          <div class="layout-breadcrumb-seting-bar-flex-label">固定 Header</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-switch v-model="getThemeConfig.isFixedHeader" @change="onIsFixedHeaderChange"></el-switch>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex mt15"
          :style="{opacity:getThemeConfig.layout !== 'classic' ? 0.5 : 1}">
          <div class="layout-breadcrumb-seting-bar-flex-label">经典布局分割菜单</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-switch v-model="getThemeConfig.isClassicSplitMenu" :disabled="getThemeConfig.layout !== 'classic'"
              @change="onClassicSplitMenuChange">
            </el-switch>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex mt15">
          <div class="layout-breadcrumb-seting-bar-flex-label">开启锁屏</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-switch v-model="getThemeConfig.isLockScreen" @change="setLocalThemeConfig"></el-switch>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex mt11">
          <div class="layout-breadcrumb-seting-bar-flex-label">自动锁屏(s/秒)</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-input-number v-model="getThemeConfig.lockScreenTime" controls-position="right" :min="0" :max="9999"
              @change="setLocalThemeConfig" size="mini" style="width:90px;">
            </el-input-number>
          </div>
        </div>

        <!-- 界面显示 -->
        <el-divider content-position="left">界面显示</el-divider>
        <div class="layout-breadcrumb-seting-bar-flex mt15">
          <div class="layout-breadcrumb-seting-bar-flex-label">侧边栏 Logo</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-switch v-model="getThemeConfig.isShowLogo" @change="onIsShowLogoChange"></el-switch>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex mt15"
          :style="{opacity:getThemeConfig.layout === 'transverse' ? 0.5 : 1}">
          <div class="layout-breadcrumb-seting-bar-flex-label">开启 Breadcrumb</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-switch v-model="getThemeConfig.isBreadcrumb" :disabled="getThemeConfig.layout === 'transverse'"
              @change="onIsBreadcrumbChange"></el-switch>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex mt15">
          <div class="layout-breadcrumb-seting-bar-flex-label">开启 Breadcrumb 图标</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-switch v-model="getThemeConfig.isBreadcrumbIcon" @change="setLocalThemeConfig"></el-switch>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex mt15">
          <div class="layout-breadcrumb-seting-bar-flex-label">开启 Tagsview</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-switch v-model="getThemeConfig.isTagsview" @change="setLocalThemeConfig"></el-switch>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex mt15">
          <div class="layout-breadcrumb-seting-bar-flex-label">开启 Tagsview 图标</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-switch v-model="getThemeConfig.isTagsviewIcon" @change="setLocalThemeConfig"></el-switch>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex mt15">
          <div class="layout-breadcrumb-seting-bar-flex-label">开启 TagsView 缓存 </div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-switch v-model="getThemeConfig.isCacheTagsView" @change="setLocalThemeConfig"></el-switch>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex mt15">
          <div class="layout-breadcrumb-seting-bar-flex-label">开启 TagsView 拖拽 </div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-switch v-model="getThemeConfig.isSortableTagsView" @change="onSortableTagsViewChange"></el-switch>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex mt15">
          <div class="layout-breadcrumb-seting-bar-flex-label">开启 Footer</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-switch v-model="getThemeConfig.isFooter" @change="setLocalThemeConfig"></el-switch>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex mt15">
          <div class="layout-breadcrumb-seting-bar-flex-label">灰色模式</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-switch v-model="getThemeConfig.isGrayscale" @change="onAddFilterChange('grayscale')"></el-switch>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex mt15">
          <div class="layout-breadcrumb-seting-bar-flex-label">色弱模式</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-switch v-model="getThemeConfig.isInvert" @change="onAddFilterChange('invert')"></el-switch>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex mt15">
          <div class="layout-breadcrumb-seting-bar-flex-label">开启水印</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-switch v-model="getThemeConfig.isWartermark" @change="onWartermarkChange"></el-switch>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex mt14">
          <div class="layout-breadcrumb-seting-bar-flex-label">水印文案</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-input v-model="getThemeConfig.wartermarkText" size="mini" style="width:90px;"
              @input="onWartermarkTextInput($event)"></el-input>
          </div>
        </div>

        <!-- 其它设置 -->
        <el-divider content-position="left">其它设置</el-divider>
        <div class="layout-breadcrumb-seting-bar-flex mt15">
          <div class="layout-breadcrumb-seting-bar-flex-label">Tagsview 风格</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-select v-model="getThemeConfig.tagsStyle" placeholder="请选择" size="mini" style="width:90px;"
              @change="setLocalThemeConfig">
              <el-option label="风格1" value="tagsStyleOne"></el-option>
              <el-option label="风格2" value="tagsStyleTwo"></el-option>
              <el-option label="风格3" value="tagsStyleThree"></el-option>
              <el-option label="风格4" value="tagsStyleFour"></el-option>
            </el-select>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex mt15">
          <div class="layout-breadcrumb-seting-bar-flex-label">主页面切换动画</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-select v-model="getThemeConfig.animation" placeholder="请选择" size="mini" style="width:90px;"
              @change="setLocalThemeConfig">
              <el-option label="slideRight" value="slideRight"></el-option>
              <el-option label="slideLeft" value="slideLeft"></el-option>
              <el-option label="opacitys" value="opacitys"></el-option>
            </el-select>
          </div>
        </div>
        <div class="layout-breadcrumb-seting-bar-flex mt15 mb28">
          <div class="layout-breadcrumb-seting-bar-flex-label">分栏高亮风格</div>
          <div class="layout-breadcrumb-seting-bar-flex-value">
            <el-select v-model="getThemeConfig.columnsAsideStyle" placeholder="请选择" size="mini" style="width:90px;"
              @change="setLocalThemeConfig">
              <el-option label="圆角" value="columnsRound"></el-option>
              <el-option label="卡片" value="columnsCard"></el-option>
            </el-select>
          </div>
        </div>

        <!-- 布局切换 -->
        <el-divider content-position="left">布局切换</el-divider>
        <div class="layout-drawer-content-flex">
          <!-- defaults 布局 -->
          <div class="layout-drawer-content-item" @click="onSetLayout('defaults')">
            <section class="el-container el-circular"
              :class="{'drawer-layout-active': getThemeConfig.layout === 'defaults'}">
              <aside class="el-aside" style="width: 20px"></aside>
              <section class="el-container is-vertical">
                <header class="el-header" style="height: 10px"></header>
                <main class="el-main"></main>
              </section>
            </section>
            <div class="layout-tips-warp" :class="{'layout-tips-warp-active': getThemeConfig.layout === 'defaults'}">
              <div class="layout-tips-box">
                <p class="layout-tips-txt">默认</p>
              </div>
            </div>
          </div>
          <!-- classic 布局 -->
          <div class="layout-drawer-content-item" @click="onSetLayout('classic')">
            <section class="el-container is-vertical el-circular"
              :class="{'drawer-layout-active': getThemeConfig.layout === 'classic'}">
              <header class="el-header" style="height: 10px"></header>
              <section class="el-container">
                <aside class="el-aside" style="width: 20px"></aside>
                <section class="el-container is-vertical">
                  <main class="el-main"></main>
                </section>
              </section>
            </section>
            <div class="layout-tips-warp" :class="{'layout-tips-warp-active': getThemeConfig.layout === 'classic'}">
              <div class="layout-tips-box">
                <p class="layout-tips-txt">经典</p>
              </div>
            </div>
          </div>
          <!-- transverse 布局 -->
          <div class="layout-drawer-content-item" @click="onSetLayout('transverse')">
            <section class="el-container is-vertical el-circular"
              :class="{'drawer-layout-active': getThemeConfig.layout === 'transverse'}">
              <header class="el-header" style="height: 10px"></header>
              <section class="el-container">
                <section class="el-container is-vertical">
                  <main class="el-main"></main>
                </section>
              </section>
            </section>
            <div class="layout-tips-warp" :class="{'layout-tips-warp-active': getThemeConfig.layout === 'transverse'}">
              <div class="layout-tips-box">
                <p class="layout-tips-txt">横向</p>
              </div>
            </div>
          </div>
          <!-- columns 布局 -->
          <div class="layout-drawer-content-item" @click="onSetLayout('columns')">
            <section class="el-container el-circular"
              :class="{'drawer-layout-active': getThemeConfig.layout === 'columns'}">
              <aside class="el-aside-dark" style="width: 10px"></aside>
              <aside class="el-aside" style="width: 20px"></aside>
              <section class="el-container is-vertical">
                <header class="el-header" style="height: 10px"></header>
                <main class="el-main"></main>
              </section>
            </section>
            <div class="layout-tips-warp" :class="{'layout-tips-warp-active': getThemeConfig.layout === 'columns'}">
              <div class="layout-tips-box">
                <p class="layout-tips-txt">分栏</p>
              </div>
            </div>
          </div>
        </div>
        <div class="copy-config">
          <el-alert title="点击下方按钮，复制布局配置去 `src/utils/themeConfig.ts` 中修改。" type="warning" :closable="false">
          </el-alert>
          <el-button size="small" class="copy-config-btn" icon="el-icon-document-copy" type="primary"
            ref="copyConfigBtnRef" @click="onCopyConfigClick($event.target)">一键复制配置
          </el-button>
        </div>
      </el-scrollbar>
    </el-drawer>
  </div>
</template>

<script lang="ts">
import {
  nextTick,
  onUnmounted,
  onMounted,
  getCurrentInstance,
  defineComponent,
  computed,
  ref,
} from "vue";
import { ElMessage } from "element-plus";
import ClipboardJS from "clipboard";
import { useStore } from "/@/store/index.ts";
import { getLightColor } from "/@/utils/theme.ts";
import Watermark from "/@/utils/wartermark.ts";
import { verifyAndSpace } from "/@/utils/toolsValidate.js";
import { setLocal, getLocal } from "/@/utils/storage.ts";
export default defineComponent({
  name: "layoutBreadcrumbSeting",
  setup() {
    const { proxy } = getCurrentInstance();
    const copyConfigBtnRef = ref();
    const store = useStore();
    // 获取布局配置信息
    const getThemeConfig = computed(() => {
      return store.state.themeConfig;
    });
    // 1、全局主题
    const onColorPickerChange = (color: string) => {
      setPropertyFun(`--color-${color}`, getThemeConfig.value[color]);
      setDispatchThemeConfig();
    };
    // 1、全局主题设置函数
    const setPropertyFun = (color: string, targetVal: any) => {
      document.documentElement.style.setProperty(color, targetVal);
      for (let i = 1; i <= 9; i++) {
        document.documentElement.style.setProperty(
          `${color}-light-${i}`,
          getLightColor(targetVal, i / 10)
        );
      }
    };
    // 2、菜单 / 顶栏
    const onBgColorPickerChange = (bg: string) => {
      document.documentElement.style.setProperty(
        `--bg-${bg}`,
        getThemeConfig.value[bg]
      );
      onTopBarGradualChange();
      onMenuBarGradualChange();
      setDispatchThemeConfig();
    };
    // 2、菜单 / 顶栏 --> 顶栏背景渐变
    const onTopBarGradualChange = () => {
      setGraduaFun(
        ".layout-navbars-breadcrumb-index",
        getThemeConfig.value.isTopBarColorGradual,
        getThemeConfig.value.topBar
      );
    };
    // 2、菜单 / 顶栏 --> 菜单背景渐变
    const onMenuBarGradualChange = () => {
      setGraduaFun(
        ".layout-container .el-aside",
        getThemeConfig.value.isMenuBarColorGradual,
        getThemeConfig.value.menuBar
      );
    };
    // 2、菜单 / 顶栏 --> 背景渐变函数
    const setGraduaFun = (el: string, bool: boolean, color: string) => {
      nextTick(() => {
        let els = document.querySelector(el);
        if (!els) return false;
        if (bool)
          els.setAttribute(
            "style",
            `background-image:linear-gradient(to bottom left , ${color}, ${getLightColor(
              color,
              0.6
            )})`
          );
        else els.setAttribute("style", `background-image:${color}`);
        setLocalThemeConfig();
        const elNavbars = document.querySelector(
          ".layout-navbars-breadcrumb-index"
        );
        const elAside = document.querySelector(".layout-container .el-aside");
        if (elNavbars) setLocal("navbarsBgStyle", elNavbars.style.cssText);
        if (elAside) setLocal("asideBgStyle", elAside.style.cssText);
      });
    };
    // 2、菜单 / 顶栏 --> 菜单字体背景高亮
    const onMenuBarHighlightChange = () => {
      nextTick(() => {
        setTimeout(() => {
          let els = document.querySelector(".el-menu-item.is-active");
          if (!els) return false;
          let attr = "el-menu-item is-active";
          if (getThemeConfig.value.isMenuBarColorHighlight)
            els.setAttribute("class", `${attr} add-is-active`);
          else els.setAttribute("class", `${attr}`);
          setLocalThemeConfig();
          setLocal("menuBarHighlightClass", els.getAttribute("class"));
        }, 0);
      });
    };
    // 3、界面设置 --> 菜单水平折叠
    const onThemeConfigChange = () => {
      onMenuBarHighlightChange();
      setDispatchThemeConfig();
    };
    // 3、界面设置 --> 固定 Header
    const onIsFixedHeaderChange = () => {
      getThemeConfig.value.isFixedHeaderChange = getThemeConfig.value
        .isFixedHeader
        ? false
        : true;
      setLocalThemeConfig();
    };
    // 3、界面设置 --> 经典布局分割菜单
    const onClassicSplitMenuChange = () => {
      getThemeConfig.value.isBreadcrumb = false;
      setLocalThemeConfig();
      proxy.mittBus.emit("getBreadcrumbIndexSetFilterRoutes");
    };
    // 4、界面显示 --> 侧边栏 Logo
    const onIsShowLogoChange = () => {
      getThemeConfig.value.isShowLogoChange = getThemeConfig.value.isShowLogo
        ? false
        : true;
      setLocalThemeConfig();
    };
    // 4、界面显示 --> 面包屑 Breadcrumb
    const onIsBreadcrumbChange = () => {
      if (getThemeConfig.value.layout === "classic") {
        getThemeConfig.value.isClassicSplitMenu = false;
      }
      setLocalThemeConfig();
    };
    // 4、界面显示 --> 开启 TagsView 拖拽
    const onSortableTagsViewChange = () => {
      proxy.mittBus.emit("openOrCloseSortable");
      setLocalThemeConfig();
    };
    // 4、界面显示 --> 灰色模式/色弱模式
    const onAddFilterChange = (attr: string) => {
      if (attr === "grayscale") {
        if (getThemeConfig.value.isGrayscale)
          getThemeConfig.value.isInvert = false;
      } else {
        if (getThemeConfig.value.isInvert)
          getThemeConfig.value.isGrayscale = false;
      }
      const cssAttr =
        attr === "grayscale"
          ? `grayscale(${getThemeConfig.value.isGrayscale ? 1 : 0})`
          : `invert(${getThemeConfig.value.isInvert ? "80%" : "0%"})`;
      document
        .getElementById("app")
        .setAttribute("style", `filter: ${cssAttr}`);
      setLocalThemeConfig();
      setLocal("appFilterStyle", document.querySelector("#app").style.cssText);
    };
    // 4、界面显示 --> 开启水印
    const onWartermarkChange = () => {
      getThemeConfig.value.isWartermark
        ? Watermark.set(getThemeConfig.value.wartermarkText)
        : Watermark.del();
      setLocalThemeConfig();
    };
    // 4、界面显示 --> 水印文案
    const onWartermarkTextInput = (val: string) => {
      getThemeConfig.value.wartermarkText = verifyAndSpace(val);
      if (getThemeConfig.value.wartermarkText === "") return false;
      if (getThemeConfig.value.isWartermark)
        Watermark.set(getThemeConfig.value.wartermarkText);
      setLocalThemeConfig();
    };
    // 5、布局切换
    const onSetLayout = (layout: string) => {
      setLocal("oldLayout", layout);
      if (getThemeConfig.value.layout === layout) return false;
      getThemeConfig.value.layout = layout;
      getThemeConfig.value.isDrawer = false;
      initSetLayoutChange();
      onMenuBarHighlightChange();
    };
    // 设置布局切换，重置主题样式
    const initSetLayoutChange = () => {
      if (getThemeConfig.value.layout === "classic") {
        getThemeConfig.value.isShowLogo = true;
        getThemeConfig.value.isBreadcrumb = false;
        getThemeConfig.value.isCollapse = false;
        getThemeConfig.value.isClassicSplitMenu = false;
        getThemeConfig.value.menuBar = "#FFFFFF";
        getThemeConfig.value.menuBarColor = "#606266";
        getThemeConfig.value.topBar = "#ffffff";
        getThemeConfig.value.topBarColor = "#606266";
        initLayoutChangeFun();
      } else if (getThemeConfig.value.layout === "transverse") {
        getThemeConfig.value.isShowLogo = true;
        getThemeConfig.value.isBreadcrumb = false;
        getThemeConfig.value.isCollapse = false;
        getThemeConfig.value.isTagsview = false;
        getThemeConfig.value.isClassicSplitMenu = false;
        getThemeConfig.value.menuBarColor = "#FFFFFF";
        getThemeConfig.value.topBar = "#545c64";
        getThemeConfig.value.topBarColor = "#FFFFFF";
        initLayoutChangeFun();
      } else if (getThemeConfig.value.layout === "columns") {
        getThemeConfig.value.isShowLogo = true;
        getThemeConfig.value.isBreadcrumb = true;
        getThemeConfig.value.isCollapse = false;
        getThemeConfig.value.isTagsview = true;
        getThemeConfig.value.isClassicSplitMenu = false;
        getThemeConfig.value.menuBar = "#FFFFFF";
        getThemeConfig.value.menuBarColor = "#606266";
        getThemeConfig.value.topBar = "#ffffff";
        getThemeConfig.value.topBarColor = "#606266";
        initLayoutChangeFun();
      } else {
        getThemeConfig.value.isShowLogo = false;
        getThemeConfig.value.isBreadcrumb = true;
        getThemeConfig.value.isCollapse = false;
        getThemeConfig.value.isTagsview = true;
        getThemeConfig.value.isClassicSplitMenu = false;
        getThemeConfig.value.menuBar = "#545c64";
        getThemeConfig.value.menuBarColor = "#eaeaea";
        getThemeConfig.value.topBar = "#FFFFFF";
        getThemeConfig.value.topBarColor = "#606266";
        initLayoutChangeFun();
      }
    };
    // 设置布局切换函数
    const initLayoutChangeFun = () => {
      onBgColorPickerChange("menuBar");
      onBgColorPickerChange("menuBarColor");
      onBgColorPickerChange("topBar");
      onBgColorPickerChange("topBarColor");
    };
    // 关闭弹窗时，初始化变量。变量用于处理 proxy.$refs.layoutScrollbarRef.update()
    const onDrawerClose = () => {
      getThemeConfig.value.isFixedHeaderChange = false;
      getThemeConfig.value.isShowLogoChange = false;
      getThemeConfig.value.isDrawer = false;
      setLocalThemeConfig();
    };
    // 布局配置弹窗打开
    const openDrawer = () => {
      getThemeConfig.value.isDrawer = true;
      nextTick(() => {
        // 初始化复制功能，防止点击两次才可以复制
        onCopyConfigClick(copyConfigBtnRef.value.$el);
      });
    };
    // 触发 store 布局配置更新
    const setDispatchThemeConfig = () => {
      setLocalThemeConfig();
      setLocalThemeConfigStyle();
    };
    // 存储布局配置
    const setLocalThemeConfig = () => {
      setLocal("themeConfig", getThemeConfig.value);
    };
    // 存储布局配置全局主题样式（html根标签）
    const setLocalThemeConfigStyle = () => {
      setLocal("themeConfigStyle", document.documentElement.style.cssText);
    };
    // 一键复制配置
    const onCopyConfigClick = (target: any) => {
      let copyThemeConfig = getLocal("themeConfig");
      copyThemeConfig.isDrawer = false;
      const clipboard = new ClipboardJS(target, {
        text: () => JSON.stringify(copyThemeConfig),
      });
      clipboard.on("success", () => {
        getThemeConfig.value.isDrawer = false;
        ElMessage.success("复制成功！");
        clipboard.destroy();
      });
      clipboard.on("error", () => {
        ElMessage.error("复制失败！");
        clipboard.destroy();
      });
    };
    onMounted(() => {
      nextTick(() => {
        // 监听菜单点击，菜单字体背景高亮
        proxy.mittBus.on("onMenuClick", () => {
          onMenuBarHighlightChange();
        });
        // 监听窗口大小改变，非默认布局，设置成默认布局（适配移动端）
        proxy.mittBus.on("layoutMobileResize", (res) => {
          if (getThemeConfig.value.layout === res.layout) return false;
          getThemeConfig.value.layout = res.layout;
          getThemeConfig.value.isDrawer = false;
          initSetLayoutChange();
          onMenuBarHighlightChange();
          getThemeConfig.value.isCollapse = false;
        });
        // 刷新页面时，设置了值，直接取缓存中的值进行初始化
        setTimeout(() => {
          // 顶栏背景渐变
          if (getLocal("navbarsBgStyle")) {
            document.querySelector(
              ".layout-navbars-breadcrumb-index"
            ).style.cssText = getLocal("navbarsBgStyle");
          }
          // 菜单背景渐变
          if (getLocal("asideBgStyle")) {
            document.querySelector(
              ".layout-container .el-aside"
            ).style.cssText = getLocal("asideBgStyle");
          }
          // 菜单字体背景高亮
          if (getLocal("menuBarHighlightClass")) {
            let els = document.querySelector(".el-menu-item.is-active");
            if (!els) return false;
            els.setAttribute("class", getLocal("menuBarHighlightClass"));
          }
          // 灰色模式/色弱模式
          if (getLocal("appFilterStyle")) {
            document.querySelector("#app").style.cssText = getLocal(
              "appFilterStyle"
            );
          }
          // 开启水印
          onWartermarkChange();
        }, 300);
      });
    });
    onUnmounted(() => {
      // 取消监听菜单点击，菜单字体背景高亮
      proxy.mittBus.off("onMenuClick");
      proxy.mittBus.off("layoutMobileResize");
    });
    return {
      openDrawer,
      onColorPickerChange,
      onBgColorPickerChange,
      onTopBarGradualChange,
      onMenuBarGradualChange,
      onMenuBarHighlightChange,
      onThemeConfigChange,
      onIsFixedHeaderChange,
      onIsShowLogoChange,
      getThemeConfig,
      onDrawerClose,
      onAddFilterChange,
      onWartermarkChange,
      onWartermarkTextInput,
      onSetLayout,
      setLocalThemeConfig,
      onClassicSplitMenuChange,
      onIsBreadcrumbChange,
      onSortableTagsViewChange,
      copyConfigBtnRef,
      onCopyConfigClick,
    };
  },
});
</script>

<style scoped lang="scss">
.layout-breadcrumb-seting-bar {
  height: calc(100vh - 50px);
  padding: 0 15px;
  ::v-deep(.el-scrollbar__view) {
    overflow-x: hidden !important;
  }
  .layout-breadcrumb-seting-bar-flex {
    display: flex;
    align-items: center;
    &-label {
      flex: 1;
      color: #666666;
    }
  }
  .layout-drawer-content-flex {
    overflow: hidden;
    display: flex;
    flex-wrap: wrap;
    align-content: flex-start;
    margin: 0 -5px;
    .layout-drawer-content-item {
      width: 50%;
      height: 70px;
      cursor: pointer;
      border: 1px solid transparent;
      position: relative;
      padding: 5px;
      .el-container {
        height: 100%;
        .el-aside-dark {
          background-color: #b3c0d1;
        }
        .el-aside {
          background-color: #d3dce6;
        }
        .el-header {
          background-color: #b3c0d1;
        }
        .el-main {
          background-color: #e9eef3;
        }
      }
      .el-circular {
        border-radius: 2px;
        overflow: hidden;
        border: 1px solid transparent;
        transition: all 0.3s ease-in-out;
      }
      .drawer-layout-active {
        border: 1px solid;
        border-color: var(--color-primary);
      }
      .layout-tips-warp,
      .layout-tips-warp-active {
        transition: all 0.3s ease-in-out;
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
        border: 1px solid;
        border-color: var(--color-primary-light-4);
        border-radius: 100%;
        padding: 4px;
        .layout-tips-box {
          transition: inherit;
          width: 30px;
          height: 30px;
          z-index: 9;
          border: 1px solid;
          border-color: var(--color-primary-light-4);
          border-radius: 100%;
          .layout-tips-txt {
            transition: inherit;
            position: relative;
            top: 5px;
            font-size: 12px;
            line-height: 1;
            letter-spacing: 2px;
            white-space: nowrap;
            color: var(--color-primary-light-4);
            text-align: center;
            transform: rotate(30deg);
            left: -1px;
            background-color: #e9eef3;
            width: 32px;
            height: 17px;
            line-height: 17px;
          }
        }
      }
      .layout-tips-warp-active {
        border: 1px solid;
        border-color: var(--color-primary);
        .layout-tips-box {
          border: 1px solid;
          border-color: var(--color-primary);
          .layout-tips-txt {
            color: var(--color-primary) !important;
            background-color: #e9eef3 !important;
          }
        }
      }
      &:hover {
        .el-circular {
          transition: all 0.3s ease-in-out;
          border: 1px solid;
          border-color: var(--color-primary);
        }
        .layout-tips-warp {
          transition: all 0.3s ease-in-out;
          border-color: var(--color-primary);
          .layout-tips-box {
            transition: inherit;
            border-color: var(--color-primary);
            .layout-tips-txt {
              transition: inherit;
              color: var(--color-primary) !important;
              background-color: #e9eef3 !important;
            }
          }
        }
      }
    }
  }
  .copy-config {
    margin: 10px 0;
    .copy-config-btn {
      width: 100%;
      margin-top: 15px;
    }
    .copy-config-last-btn {
      margin: 10px 0 0;
    }
  }
}
</style>