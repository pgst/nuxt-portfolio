<script setup>
const blogsPerPage = 5;

const { data } = await useAsyncData('blogQuery', () =>
  queryContent('/blog').sort({ id: -1 }).limit(blogsPerPage).find()
);

const allBlogs = await queryContent('/blog').find();
const numberPages = Math.ceil(allBlogs.length / blogsPerPage);

useHead({
  title: 'ブログ',
  meta: [
    {
      name: 'description',
      content: 'ブログページです',
    },
  ],
});
</script>

<template>
  <div class="wrapper">
    <div class="container">
      <h1>Blog</h1>
      <p>エンジニアの日常生活をお届けします</p>
      <div v-for="singleData in data" :key="singleData.id" class="blogCard">
        <div class="textsContainer">
          <h3>{{ singleData.title }}</h3>
          <p>{{ singleData.excerpt }}</p>
          <p>{{ singleData.date }}</p>
          <NuxtLink :to="singleData._path" class="linkButton"
            >Read More</NuxtLink
          >
        </div>
        <div class="blogImg">
          <nuxt-img :src="singleData.image" alt="blog-image" format="webp" />
        </div>
      </div>
    </div>
    <Pagination :numberPages="numberPages" />
  </div>
</template>
