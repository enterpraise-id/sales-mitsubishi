<script lang="ts" setup>
import usePaginationGetter from '../composable/usePaginationGetter';
import Button from './Button.vue';
import NewsCard from './NewsCard.vue'
import { News } from '../typings/News';
import { METHODS } from 'http';
import Pagination from './Pagination/Pagination.vue';


const {
  data: newsList,
  perPage,
  setPerPage,
  totalPage,
  setPage,
  setOrder: setOrderNews,
} = usePaginationGetter<News>({
  path: "news",
  perPage: 5,
  autoFetch: true,
});

const orderNewsBy = (order: string) => {
  if (order === "latest") {
    setOrderNews("created_at", false);
  }

  if (order === "popular") {
  }
};

const loadMoreNews = () => {
  setPerPage(perPage.value + 5);
};
const loadLessNews = () => {
  setPerPage(perPage.value - 5);
};

</script>
<template>
  <div class="relative flex justify-center py-10 bg-white">
    <div class="absolute top-0 left-0 z-[1] w-full h-full hidden md:block" />

    <div class="w-full z-[2] md:px-0">
      <div class="flex flex-col justify-between">
        <div class="w-full text-4xl font-bold text-secondary text-center">Artikel</div>
        <div class="flex gap-2 text-black justify-center mt-4">
          <a href="#" @click="orderNewsBy('latest')">Terbaru</a>
          <div>|</div>
          <a href="#" @click="orderNewsBy('popular')">Terpopuler</a>
        </div>
      </div>
      <div class="grid grid-cols-1 gap-10 mt-10 md:grid-cols-5 px-8 md:px-20">
        <NewsCard v-for="item in newsList" :key="item.slug" :data="item" />
      </div>

      <div v-if="perPage < 10" class="flex justify-center mt-10">
        <Button @click="loadMoreNews">Tampilkan Lebih Banyak</Button>
      </div>

      <div v-if="perPage === 10" class="flex justify-center mt-10">
        <Button @click="loadLessNews">Tampilkan Lebih Sedikit</Button>
      </div>
      <Pagination :with-edges="true" :with-controls="true" :total="totalPage" :per-page="perPage" @change="setPage" />

    </div>
  </div>
</template>