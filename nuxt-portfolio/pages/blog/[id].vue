<script setup>
const { data } = await useAsyncData(useRoute().path, () =>
  queryContent(useRoute().path).findOne()
);

const [prev, next] = await queryContent('/blog')
  .sort({ id: 1 })
  .findSurround(useRoute().path);
</script>

<template>
  <div>
    <div>
      <nuxt-img :src="data.image" alt="blog-image" format="webp" />
    </div>
    <div>
      <div>
        <h1>{{ data.title }}</h1>
        <p>{{ data.date }}</p>
        <ContentDoc />
      </div>
      <PrevNext :prev="prev" :next="next" />
    </div>
  </div>
</template>
