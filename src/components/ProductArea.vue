<script lang="ts" setup>
import usePaginationGetter from '../composable/usePaginationGetter';
// @ts-ignore
import ProductCard from "../components/ProductCard.vue";
// @ts-ignore
import Button from "../components/Button.vue";
import { Product } from '../typings/Product';
import Slider from './Slider';

const { data: products, perPage, setPerPage } = usePaginationGetter<Product>({
  path: "products",
  perPage: 3,
  autoFetch: true,
});

const options = {
  gap: 30,
  perView: 5,
  hasBullet: true,
  hasArrows: true,
  breakpoints: {
    600: {
      perView: 1
    },
    800: {
      perView: 3
    },
    1200: {
      perView: 4
    }
  }
}

const loadMoreProduct = () => {
  setPerPage(perPage.value + 3);
};
</script>

<template>
  <div id="produk" class="relative flex flex-col items-center justify-center pt-10 pb-10 bg-secondary">
    <div class="absolute z-[1] top-0 left-0 h-full w-full bg-secondary" />
    <div class="flex items-center justify-center w-full max-w-screen-lg static z-[2] px-4">
      <div>
        <h5 class="text-3xl font-bold text-primary">Produk Kami</h5>
      </div>
    </div>
    <div class="z-10 w-full px-8 md:px-20 mt-10">
      <Slider id="product-slider" :items="products" :options="options">
        <template #item="{ item, classes }">
          <li :class="classes">
            <ProductCard :data="item" />
          </li>
        </template>
      </Slider>
    </div>
    <div class="z-[10] mt-10">
      <Button @click="loadMoreProduct">Tampilkan Lebih Banyak</Button>
    </div>
  </div>
</template>

<style scoped>
.clip-3 {
  clip-path: polygon(0% 0%, 35% 0%, 60% 100%, 0% 100%);
}
</style>