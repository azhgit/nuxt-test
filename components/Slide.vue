<template>
  <div class="relative w-full mx-auto border-4 border-yellow-300 sm:w-4/5 rounded-2xl">
    <div class="justify-center block px-12 py-5 text-center lg:flex row">
      <div class="m-auto overflow-hidden lg:w-1/2 swiper-container-test-announcement">
        <!-- Additional required wrapper -->
        <div class="swiper-wrapper">
          <!-- Slides -->
          <div v-for="item in picList" :key="item.url" class=" swiper-slide">
            <a class="block w-full bg-center bg-no-repeat bg-cover banner_item" :style="{ backgroundImage: 'url(' + item.url + ')'}" target="_blank">
            </a>
          </div>
        </div>
      </div>
      <div class="absolute w-full h-full transform -translate-x-1/2 -translate-y-1/2 custom-swiper-btn top-1/2 left-1/2">
        <div class="bg-center bg-no-repeat bg-contain swiper-button-prev"></div>
        <div class="bg-center bg-no-repeat bg-contain swiper-button-next"></div>
      </div>
      <div class="w-full p-5 m-auto text-center lg:w-1/2 test_info">
        <div class="hidden text-4xl font-extrabold leading-5 text-center lg:block test_title sm:text-5xl">
          {{currentSlide.name}}
        </div>
        <div class="flex flex-wrap justify-between m-auto text-sm test_data sm:text-2xl">
          <div class="text-right test_data_title">ID</div>
          <div class="pl-3 text-left test_data_text">{{currentSlide.ID}}</div>
        </div>
      </div>
    </div>
  </div>
  <div class="flex text-center row justify-evenly">
    <div v-for="item in data" :key="item.url" class="">
      <img :src="item.url" alt />
    </div>
  </div>
</template>

<script setup>
  import Swiper, { Navigation, Autoplay } from 'swiper'
  Swiper.use([Navigation, Autoplay])
  let currentSlide = ref({});
  let swiper = {};
  const { data:picList, pending } = await useAsyncData("getList", () =>
    $fetch("https://vue-lessons-api.herokuapp.com/photo/list")
  );
  onMounted(()=>{
    //for testing... api must offer ID 
    picList.value.forEach((item, index)=>{
      item.ID = index + 1
      item.name = `肥宅快樂水-${item.ID}`
    })
    currentSlide.value = picList.value[0];
    console.log(swiper)
    swiper = new Swiper('.swiper-container-test-announcement', {
      // loop: true,
      autoplay: {
        delay: 3500,
        stopOnLastSlide: false,
        disableOnInteraction: false
      },
      navigation: {
        nextEl: '.swiper-button-next',
        prevEl: '.swiper-button-prev'
      },
      on: {
        slideChange: function () {
          currentSlide.value =  picList.value[swiper.activeIndex];
          //console.log(swiper)
        },
      },
    });
    console.log(picList.value)
    console.log(swiper)
  });
  </script>
  
  <style lang="scss" scoped>   
  .swiper-container-test-announcement {
    .banner_item{
      height: auto;
      padding-top: 61.95% //565*350
    }
  }
  .swiper-button-prev{
    background-image: url(@/assets/images/arrow_left.png);
    filter: drop-shadow(0 0 3.5px rgba(255,255,255,0.6));
    left:8px;
  }
  .swiper-button-next{
    background-image: url(@/assets/images/arrow_right.png);
    filter: drop-shadow(0 0 3.5px rgba(255,255,255,0.6));
    right:8px;
  }
  .swiper-button-prev:after, .swiper-button-next:after{
    // color: #ffff00;
    // font-size: 25px;
    display: none;
  }
  .test_info{
    max-width:450px ;
  }
  .test_title{
    // text-align: center;
    // font-weight:800;
    // font-size: 3rem;
    // line-height: 1.2em;
    color: black;
  }

  .test_data {
    margin: auto;
    
    display:flex;
    justify-content:space-between;
    flex-wrap:wrap;
    // font-size: 1.5rem;
    // line-height: 1.6rem;
    // text-shadow: rgb(24, 0, 0)  3px 5px 2px;
    @media (max-width: 371px) {
      font-size: 0.75rem; 
      line-height: 1rem;
    }
  .test_data_title {
    width: 35%;
    color: rgb(255, 0, 0);
    font-weight:800;

  }
  .test_data_text {
    color:black;
    width: 65%;
  }

}
.test_time {
  background-color: rgba(0, 0, 0, 0.8);
  border-radius: 40px;
  border:  1px solid rgba(112, 0, 0, 0.8);
  color: white;
}
  </style>