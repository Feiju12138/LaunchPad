<template>
  <div v-if="store.siteLinks[0]" class="links">
    <!-- 网站列表 -->
    <Swiper
        v-if="store.siteLinks[0]"
        :modules="[Pagination, Mousewheel]"
        :slides-per-view="1"
        :space-between="40"
        :pagination="{
        el: '.swiper-pagination',
        clickable: true,
        bulletElement: 'div',
      }"
        :mousewheel="true"
    >
      <SwiperSlide v-for="site in siteLinksList" :key="site">
        <el-row class="link-all" :gutter="20">
          <el-col v-for="(item, index) in site" :span="4" :key="item">
            <div
                class="item cards"
                :style="index < 24 ? 'margin-bottom: 20px' : null"
                @click="jumpLink(item)"
            >
              <Icon size="26">
                <component :is="siteIcon[item.icon]"/>
              </Icon>
              <span class="name text-hidden">{{ item.name }}</span>
            </div>
          </el-col>
        </el-row>
      </SwiperSlide>
      <div class="swiper-pagination"/>
    </Swiper>
  </div>
</template>

<script setup>
import {Icon} from "@vicons/utils";
import { Swiper, SwiperSlide } from "swiper/vue";
import { Pagination, Mousewheel } from "swiper/modules";

import { mainStore } from "@/store";
const store = mainStore();

// 网站链接图标
// 可前往 https://www.xicons.org 自行挑选并在此处引入
import {
  Blog,
  CloudDownloadAlt,
  CloudUploadAlt,
  SyncAlt,
  Cloud,
  Server,
  PhotoVideo,
  Gamepad,
  Home,
  Docker,
  Book,
  Camera,
  Film,
  Search,
  PaintBrush,
  GitAlt,
  Music,
  File,
  NetworkWired,
  ClipboardList
} from "@vicons/fa"; // 注意使用正确的类别
const siteIcon = {
  Blog,
  CloudDownloadAlt,
  CloudUploadAlt,
  SyncAlt,
  Cloud,
  Server,
  PhotoVideo,
  Gamepad,
  Home,
  Docker,
  Book,
  Camera,
  Film,
  Search,
  PaintBrush,
  GitAlt,
  Music,
  File,
  NetworkWired,
  ClipboardList,
};

// 计算网站链接
const siteLinksList = computed(() => {
  const siteLinks = store.siteLinks;
  const result = [];
  for (let i = 0; i < siteLinks.length; i += 24) {
    const subArr = siteLinks.slice(i, i + 24);
    result.push(subArr);
  }
  return result;
});

// 链接跳转
const jumpLink = (data) => {
  window.open(data.link, "_blank");
};
</script>

<style lang="scss" scoped>
.links {
  .line {
    margin: 2rem 0.25rem 1rem;
    font-size: 1.1rem;
    display: flex;
    align-items: center;
    animation: fade 0.5s;

    .title {
      margin-left: 8px;
      font-size: 1.15rem;
      text-shadow: 0 0 5px #00000050;
    }
  }

  .swiper {
    left: -10px;
    width: calc(100% + 20px);
    padding: 5px 10px 0;
    z-index: 0;

    .swiper-slide {
      height: 100%;
    }

    .swiper-pagination {
      margin-top: 12px;
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: center;

      :deep(.swiper-pagination-bullet) {
        background-color: #fff;
        width: 20px;
        height: 4px;
        margin: 0 4px;
        border-radius: 4px;
        opacity: 0.2;
        transition: opacity 0.3s;

        &.swiper-pagination-bullet-active {
          opacity: 1;
        }

        &:hover {
          opacity: 1;
        }
      }
    }
  }

  .link-all {
    height: 100%;

    .item {
      height: 100px;
      width: 100%;
      display: flex;
      align-items: center;
      flex-direction: row;
      justify-content: center;
      padding: 0 10px;
      animation: fade 0.5s;

      &:hover {
        transform: scale(1.02);
        background: rgb(0 0 0 / 40%);
        transition: 0.3s;
      }

      &:active {
        transform: scale(1);
      }

      .name {
        font-size: 1.1rem;
        margin-left: 8px;
      }

      @media (min-width: 720px) and (max-width: 820px) {
        .name {
          display: none;
        }
      }
      @media (max-width: 720px) {
        height: 80px;
      }
      @media (max-width: 460px) {
        flex-direction: column;
        .name {
          font-size: 1rem;
          margin-left: 0;
          margin-top: 8px;
        }
      }
    }

    @media (max-width: 720px) {
      height: 180px;
    }
  }
}
</style>
