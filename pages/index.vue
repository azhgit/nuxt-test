<template>
  <div class="relative">
    <div class="absolute top-0 left-0 z-20 w-full h-full bg-repeat opacity-25 body-bg"></div>
    <div class="absolute top-0 left-0 z-10 w-full h-full body-bg2"></div>
    <div class="container relative z-30 p-8 mx-auto border-2 border-white border-solid ">
      <!-- <WinnerAnnouncement /> -->
      <WinnerAnnouncement2 />
    </div>
  </div>
</template>
<script setup>

</script>

<style lang="scss" scoped>

.body-bg{
  background-image: url(@/assets/images/bg_texture.png);
  background-size: 80px;
}
.body-bg2{
  background-image: linear-gradient(to right, rgba(0,0,0,0.93) 0%,rgba(104,0,0,0.93) 25%,rgba(170,0,0,0.93) 50%,rgba(104,0,0,0.93) 74%,rgba(0,0,0,0.93) 100%);
}


</style>
