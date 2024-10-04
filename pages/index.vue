<template>
  <div class="wrap">
    <h1>Nuxt3 microCMS Jamstack</h1>
    <ul class="home-list">
      <li v-for="blog in data?.contents" :key="blog.id">
        <NuxtLink :to="`/${blog.id}`">
          <img
            :src="blog.eyecatch?.url"
            :width="blog.eyecatch?.width"
            :height="blog.eyecatch?.height"
            alt=""
            class="thumb"
          />
          <div>
            <div class="tag">
              {{ blog.category?.name }}
            </div>
            <div>
              {{ blog.title }}
            </div>
            <div class="days">
              {{ dateFormat(blog.publishedAt ?? blog.createdAt) }}
            </div>
          </div>
        </NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
  import { Blog } from "~~/types/blog";
  import { useHead } from "#app";
  const config = useRuntimeConfig();


  const { data } = await useMicroCMSGetList<Blog>({
    endpoint: "blogs",
  });

  useHead({
    title: `${config.public.siteName}`,
  });
</script>


<style scoped>
.thumb {
  border-radius: 0.5rem;
  overflow: hidden;
  margin-bottom: 1.5em;
}

</style>