<template>
  <div class="flex justify-center row">
    <img class="w-4/5 md:w-3/5" src="/assets/images/title/title_games.png" alt />
  </div>
  <div class="relative w-full mx-auto border-4 border-yellow-300 sm:w-4/5 rounded-2xl">
    <div class="justify-center block px-12 py-5 text-center lg:flex row">
      <div class="m-auto overflow-hidden lg:w-1/2 swiper-container-winner-announcement">
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
      <div class="w-full p-5 m-auto text-center lg:w-1/2 winner_info">
        <div class="hidden text-4xl font-extrabold leading-5 text-center lg:block winning_title sm:text-5xl">
          埃及豔后
          <hr class="winning_title_hr">
        </div>
        <div class="flex flex-wrap justify-between m-auto text-sm winning_data sm:text-2xl">
          <div class="text-right winning_data_title">恭喜玩家</div>
          <div class="pl-3 text-left winning_data_text">{{getWinnerInfo('name')}}</div>
          <div class="text-right winning_data_title">奪得大獎</div>
          <div class="pl-3 text-left winning_data_text">42,708,000</div>
          <div class="text-right winning_data_title">機台編號</div>
          <div class="pl-3 text-left winning_data_text">38</div>
        </div>
        <div class="mt-3 text-sm text-center winning_time sm:text-2xl">
          <span class="winning_time_title">得獎時間</span>
          <span class="winning_time_day">2022/08/03</span>
        </div>
      </div>
    </div>
    <!-- <div class="flex text-center row justify-evenly">
      <div>6666</div>
      <div>
        <div>埃及豔后</div>
        <div>玩家 發財金</div>
        <div>傳奇巨獎</div>
        <div>8,266,000</div>
      </div>
    </div> -->
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
  
  const { data } = await useAsyncData("getList", () =>
    $fetch("https://vue-lessons-api.herokuapp.com/photo/list")
  );
  // console.log(data);
  const { data:picList, pending } = await useAsyncData("getList", () =>
    $fetch("https://vue-lessons-api.herokuapp.com/photo/list")
  );
  onMounted(()=>{
    //for testing... api must offer ID 
    picList.value.forEach((item, index)=>{
      item.ID = index + 1
      item.name = `肥宅快樂水-${item.ID}`
      item.prize = `42,708,000-${item.ID}`
      item.machine = `38-${item.ID}`
      item.time = `2022/08/03-${item.ID}`
      console.log(item)

    })
    const swiper = new Swiper('.swiper-container-winner-announcement', {
      loop: true,
      // autoplay: {
      //   delay: 3500,
      //   stopOnLastSlide: false,
      //   disableOnInteraction: false
      // },
      navigation: {
        nextEl: '.swiper-button-next',
        prevEl: '.swiper-button-prev'
      }
    });
  });
  const getWinnerInfo = (type)=>{
    console.log(type)
    return '5566'
  }
  </script>
  
  <style lang="scss" scoped>   
  .swiper-container-winner-announcement {
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
  .winner_info{
    max-width:450px ;
  }
  .winning_title{
    // text-align: center;
    // font-weight:800;
    // font-size: 3rem;
    // line-height: 1.2em;
    color: rgb(255, 245, 233);
    text-shadow: rgb(71, 0, 0) 0px -1px 4px,rgba(255, 255, 255, 0.472) 0px -1px 4px, rgb(255, 255, 0) 0px -2px 10px, rgb(255, 128, 0) 0px -10px 20px, rgb(255, 0, 0) 0px -18px 40px;
  }
  .winning_title_hr{
    border: 0;
    height: 1px;
    background-image: linear-gradient(to right, rgba(50, 0, 0, 0.5), rgb(255, 208, 0), rgba(50, 0, 0, 0.5));
    margin: 0.3em 0;
  }

  .winning_data {
    margin: auto;
    
    display:flex;
    justify-content:space-between;
    flex-wrap:wrap;
    // font-size: 1.5rem;
    // line-height: 1.6rem;
    // text-shadow: rgb(24, 0, 0)  3px 5px 2px;
    // @media screen and (max-width: 486px){
    //   font-size: 1rem;
    //   line-height: 1rem;
    // }
  .winning_data_title {
    width: 35%;
    color: rgb(255, 0, 0);
    font-weight:800;

  }
  .winning_data_text {
    color:white;
    width: 65%;
  }

}
.winning_time {
  background-color: rgba(0, 0, 0, 0.8);
  border-radius: 40px;
  border:  1px solid rgba(112, 0, 0, 0.8);
  color: white;
}
  </style>