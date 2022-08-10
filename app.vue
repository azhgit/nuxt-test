<template>
  <div>
    <Head>
      <Title>Andrew's App</Title>
      <Meta name="description" content="Andrew app description" />
      <Meta property="og:image" content="https://www.7dd168.com/AppIcon.png" />
      <Meta property="og:title" content="錢多多娛樂城-經典呈現實體遊藝場機台" />
      <Meta
        property="og:description"
        content="業界唯一視訊機台｜齊天大聖。經典呈現台灣原汁味的遊藝場機台，超多玩法讓您選！超高中獎率，手機、電腦可同步，24小時任你玩，讓你走到哪玩到哪，為玩家客製的線上遊藝場，為您打造經典傳奇！"
      />
    </Head>
    <NuxtLayout :name="layout">
      <NuxtPage />
    </NuxtLayout>
  </div>
</template>

<script setup>
// You might choose this based on an API call or logged-in status
const layout = "default";
</script>
