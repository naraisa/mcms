<template>
  <template v-if="data">
    <div class="wrap">
    <h1>
      {{ data.title }}
    </h1>
    <img
      :src="data.eyecatch?.url"
      :width="data.eyecatch?.width"
      :height="data.eyecatch?.height"
      alt=""
    />
    <div>
      <div>
        {{ data.category?.name }}
      </div>
      <div>
        {{ dateFormat(data.publishedAt ?? data.createdAt) }}
      </div>
    </div>
    <div v-html="data.content"></div>
    </div>
  </template>
</template>

<script setup lang="ts">
import { Blog } from "~~/types/blog";
import { useHead } from "#app";
import { useRoute, useRuntimeConfig } from "#app";

const { params } = useRoute();
const config = useRuntimeConfig();

const { data } = await useMicroCMSGetListDetail<Blog>({
  endpoint: "blogs",
  contentId: Array.isArray(params.id) ? params.id[0] : params.id,
});


if (data) {
  // console.log(data.value.title)
  const currentUrl = `${config.app.baseURL}${params.id}`; // 現在のページのURLを作成
  console.log(config.app.baseURL)
  console.log(currentUrl)
  useHead({
    title: data.value.title,
    // meta: [
    //   {
    //     property: "og:url",
    //     content: currentUrl, // og:urlに設定
    //   },
    //   {
    //     property: "og:title",
    //     content: data.title, // og:titleにも設定
    //   },
    // ],
  });
}
// console.log(data)
</script>