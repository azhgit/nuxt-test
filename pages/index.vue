<template>
  <div>
    <div class="container mx-auto bg-gray-300 p-8">
      <h1 class="font-bold text-gray-600 text-lg">Hello, Tailwind 3!</h1>
      <ul class="all_btn">
        <li v-for="item in data" :key="item.url">
          <img :src="item.url" alt />
        </li>
      </ul>
      <NuxtLink to="/demo">Demo.vue</NuxtLink>
    </div>
  </div>
</template>
<script setup>
const { data } = await useAsyncData("getList", () =>
  $fetch("https://vue-lessons-api.herokuapp.com/photo/list")
);
console.log(data);
</script>

<style scoped lang="scss">
.all_btn {
  list-style: none;
  margin: 0 auto;
  padding: 0;
  max-width: 1495px;
  > li {
    width: 30%;
    max-width: 594px;
    margin: 0px 5px;
    display: inline-block;
    @media (max-width: 768px) {
      width: 40%;
      // width: 45%;
      // max-width: 150px;
    }
  }
}
</style>