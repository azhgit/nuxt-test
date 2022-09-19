<script setup>
import Swiper, { Pagination, Autoplay } from 'swiper'
import { useWindowScroll, useElementBounding  } from '@vueuse/core'
import imageQrCode from '@/assets/images/sidebar/qrcode.jpg'
import imageAPK from '@/assets/images/sidebar/apk_pc.png'
import imageGooglePlay from '@/assets/images/sidebar/google_pc.png'
import imageAppStore from '@/assets/images/sidebar/apple_pc.png'
import IconUp from "~icons/heroicons-outline/arrow-circle-up";
Swiper.use([Pagination, Autoplay])


// const { x, y } = useWindowScroll()
const el = ref(null)
const { x2, y2, top, right, bottom, left, width, height } = useElementBounding(el)
const isFixed = ref(false);
const btnMenus = reactive([
        { name: '遊戲介紹', path: 'demo', test:'demo' },
        { name: '會員中心', path: 'menu2', test:'' },
        { name: '儲值購點', path: 'menu3', test:'' },
        { name: '序號兌換', path: 'menu4', test:'' },
        { name: '常見問題', path: 'menu5', test:'' }]);
const downloadInfo = reactive([
        {
          imageUrl: imageAPK,
          storeUrl: 'https://7dd168.onelink.me/Yn9I/Website'
        },
        {
          imageUrl: imageGooglePlay,
          storeUrl: 'https://play.google.com/store/apps/details?id=com.wmh.igame&hl=zh_TW'
        },
        {
          imageUrl: imageAppStore,
          storeUrl: 'https://apps.apple.com/tw/app/id1473765988'
        }]);

const { data:picList, pending } = await useAsyncData("getList", () =>
  $fetch("https://vue-lessons-api.herokuapp.com/photo/list")
);
// console.log(picList.value)
const upToTop = () => {
  window.scroll({
        top: 0,
        left: 0,
        behavior: 'smooth'
      })
};
onMounted(()=>{
  const swiper = new Swiper('.swiper-container', {
    loop: true,
    autoplay: {
      delay: 3500,
      stopOnLastSlide: false,
      disableOnInteraction: false
    },
    pagination: {
      el: '.swiper-pagination',
      clickable: true
    }
  });
});
watch(bottom,(newNum)=>{
  newNum > 0 ? isFixed.value = false : isFixed.value = true;
})

//const isOpen = ref(false);
// const HandMenuOpen = () => {
//   isOpen.value = !isOpen.value;
// };
</script>
<template>
  <div ref="el"  :class="{'relative': !isFixed}">
    <div class="w-full overflow-hidden bg-center bg-no-repeat bg-cover banner_box">
      <!-- absolute transform -translate-x-1/2 -translate-y-1/2 top-1/2 left-1/2 -->
      <div class="relative w-full h-full mx-auto my-0 animation_box">
        <div class="absolute hidden transform -translate-x-1/2 -translate-y-1/2 md:block logo left-1/2">
          <img class="" src="/assets/images/BRC_LOGO.png" alt />
        </div>
        <div v-if="!pending" class="absolute transform -translate-x-1/2 -translate-y-1/2 left-1/2 slides">
          <div class="swiper-container">
          <!-- Additional required wrapper -->
          <div class="swiper-wrapper">
            <!-- Slides -->
            <div v-for="item in picList" :key="item.url" class="swiper-slide">
              <a class="w-full bg-center bg-no-repeat bg-cover banner_item" :style="{ backgroundImage: 'url(' + item.url + ')'}" target="_blank">
              </a>
            </div>
          </div>
          <!-- If we need pagination -->
          <div class="swiper-pagination"></div>
    
          <!-- If we need navigation buttons -->
          <!-- <div class="swiper-button-prev"></div>
          <div class="swiper-button-next"></div> -->
    
          <!-- If we need scrollbar -->
          <!-- <div class="swiper-scrollbar"></div> -->
          </div>
        </div>
        <div class="absolute hidden w-full transform -translate-x-1/2 -translate-y-1/2 md:block menu_btns left-1/2">
          <div class="flex text-center row justify-evenly">
            <ul class="list-none all_btn">
              <li class="inline-block mx-1 my-0" v-for="item in btnMenus" :key="item.name">
                <NuxtLink class="block px-2 bg-center bg-no-repeat bg-cover cursor-pointer tag-style" :class="item.path" :to="'/'+item.test"></NuxtLink>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
    <div class="z-40 justify-center hidden py-2 text-center md:flex md:flex-col right-4 sidebar" :class="{'fixed top-0': isFixed,'absolute top-100': !isFixed}">
      <div class="mt-1 font-medium text-center text-white bold">
        手機立刻下載
      </div>
      <div
        class="p-2 mx-1 my-1"
      >
        <img :src="imageQrCode"  />
      </div>
      <div
        v-for="item in downloadInfo"
        :key="item.storeUrl"
        class="px-2 mx-1 my-1"
      >
        <a :href="item.storeUrl" target="_blank">
          <img :src="item.imageUrl"  />
        </a>
      </div>
      <div class="flex items-center justify-center my-2 text-white" @click="upToTop">
        <icon-up class="w-8 h-8 text-white" />
        <span class="ml-2 font-semibold">TOP</span>
      </div>
    </div>
  </div>
  <!-- <header :class="{ openMenu: isOpen }">
    <nav>
      <h1>Mike</h1>
      <NuxtLink class="Title" to="/">Mike</NuxtLink>
      <a id="moblie_menu" @click="HandMenuOpen" href></a>
      <div>
        <NuxtLink to="/rwd">RWD</NuxtLink>
        <NuxtLink to="/vuejs">VUEJS</NuxtLink>
        <NuxtLink to="/reactjs">REACTJS</NuxtLink>
        <NuxtLink to="/html5">HTML5</NuxtLink>
        <NuxtLink to="/nodejs">NODEJS</NuxtLink>
      </div>
    </nav>
  </header> -->
</template>
<style lang="scss" scoped>
.banner_box{
  height:600px; 
  background-image: url(/assets/images/testHeaderBg.jpg);
  @media (max-width: 1200px) {
    height: auto;
    padding-top: 50%;
  }
}
.animation_box{
  border: red solid;
  max-width: 1200px;
  @media (max-width: 1200px) {
    width: 100%;
    height: 100%;
    position: absolute;
    left: 0;
    top: 0;
  }
  .logo{
    width: 20%;
    top: 12%;
  }
  .slides{
    border:#f7e76b solid 6px;
    width: 83.33%;
    top: 52.5%;
  }
  .menu_btns{
    border:#f7e76b solid;
    max-width: 1100px;
    top: 92%;  
    .all_btn{
      >li{
        width: 200px;
        @media (max-width: 1061px) {
          width: 140px;
        }
        .tag-style{
          padding-top: 33.73%;
          &.demo{
            background-image: url(@/assets/images/menu/b1.png);
            &.router-link-exact-active{
              background-image: url(@/assets/images/menu/b1_active.png);
            }
          }
          &.menu2{
            background-image: url(@/assets/images/menu/b2.png);
            &.router-link-exact-active{
              background-image: url(@/assets/images/menu/b2_active.png);
            }
          }
          &.menu3{
            background-image: url(@/assets/images/menu/b3.png);
            &.router-link-exact-active{
              background-image: url(@/assets/images/menu/b3_active.png);
            }
          }
          &.menu4{
            background-image: url(@/assets/images/menu/b4.png);
            &.router-link-exact-active{
              background-image: url(@/assets/images/menu/b4_active.png);
            }
          }
          &.menu5{
            background-image: url(@/assets/images/menu/b5.png);
            &.router-link-exact-active{
              background-image: url(@/assets/images/menu/b5_active.png);
            }
          }
        }
      }
    }  
  }
}
.swiper-container {
  // height: 350px;
  .banner_item{
    height: 350px;
    display: block;
    // background-position: center;
    // background-size: cover;
    @media (max-width: 1200px) {
      height: auto;
      padding-top: 35%
    }
  }
}
.swiper-button-prev:after, .swiper-button-next:after{
  display: none;
}
.swiper-pagination-bullet-active{
  color: #ffff00 !important;
}
.swiper-pagination :deep(.swiper-pagination-bullet){
    width: 10px;
    height: 10px;
    background-color: #070707;
}
.swiper-pagination :deep(.swiper-pagination-bullet-active){
    width: 10px;
    height: 10px;
    background-color: #ffff00;
}
.sidebar{
  width: 175px;
  background-color: #00000077;
  @media (max-width: 1330px) {
    width: 140px;
  }
  border: 2px solid #fff;
  border-color: #fff;
  border-radius:10px;
}












h6 {
  color: greenyellow;
  font-size: 40px;
}
header {
  background-color: #373c3f;
  width: 100%;
  height: 97px;
  @media screen and (max-width: 640px) {
    transition: height 0.2s;
    height: 37px;
    overflow: hidden;
    &.openMenu {
      height: 232px;
    }
  }
  > nav {
    position: relative;
    width: 1024px;
    height: 100%;
    margin: 0 auto;
    @media screen and (max-width: 1044px) {
      width: 100%;
    }
    @media screen and (max-width: 640px) {
      width: 100%;
      height: 232px;
    }
    > .Title {
      line-height: 97px;
      font-size: 18px;
      float: left;
      color: #fff;
      margin-right: 20px;
      @media screen and (max-width: 1044px) {
        margin-left: 5%;
      }
      @media screen and (max-width: 640px) {
        line-height: 37px;
      }
    }
    > div {
      width: 100%;
      height: 100%;
      @media screen and (max-width: 640px) {
        clear: both;
        width: 100%;
        height: 195px;
      }
      > a {
        display: block;
        line-height: 97px;
        font-size: 15px;
        float: left;
        color: #fff;
        padding: 0 10px;
        @media screen and (max-width: 640px) {
          width: 100%;
          height: auto;
          overflow: hidden;
          line-height: 37px;
          text-align: center;
        }
      }
    }
  }
}
a#moblie_menu {
  display: none;
  @media screen and (max-width: 640px) {
    position: absolute;
    top: 0;
    right: 0;
    display: block;
    width: 37px;
    height: 37px;
    background-image: url("~@/assets/images/menu.jpg");
    background-position: 50% 50%;
    background-size: 95% auto;
    background-repeat: no-repeat;
  }
}
// header > nav {
//   position: relative;
//   width: 1024px;
//   height: 100%;
//   margin: 0 auto;
// }
// header > nav > h1 {
//   line-height: 97px;
//   font-size: 18px;
//   float: left;
//   color: #fff;
//   margin-right: 20px;
// }
// header > nav > div {
//   width: 100%;
//   height: 100%;
// }
// header > nav > div > a {
//   display: block;
//   line-height: 97px;
//   font-size: 15px;
//   float: left;
//   color: #fff;
//   padding: 0 10px;
// }
</style>
