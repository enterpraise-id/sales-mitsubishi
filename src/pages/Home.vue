<script setup lang="ts">
import { onMounted} from "vue";
import useMeta from "../composable/useMeta";
// @ts-ignore
import Button from "../components/Button.vue";
// @ts-ignore
import TestimonialArea from "../components/TestimonialArea.vue";
// @ts-ignore
import ProductArea from "../components/ProductArea.vue";
// @ts-ignore
import NewsArea from "../components/NewsArea.vue";
import useHeadlineBanner from '../composable/useGetHeadlineSlider'
// @ts-ignore
import HeadlineSlider from '../components/HeadlineSlider/HeadlineSlider.vue'

const { data: mainBanners } = useHeadlineBanner();

useMeta({
  title: "Mitsubishi Jakarta Pusat",
});

onMounted(() => {
  window.scrollTo(0, 0);
});
</script>

<template>
  <HeadlineSlider :items="mainBanners"></HeadlineSlider>
  <div>
    <section id="produk">
      <ProductArea />
    </section>
    <section id="artikel">
      <NewsArea />
    </section>
    <section>
      <TestimonialArea />
    </section>
    <div class="mb-12" id="kontak">
    </div>
  </div>
</template>

<style scoped>
.clip-1 {
  clip-path: polygon(60% 0%, 100% 0%, 100% 100%, 40% 100%);
}

@media screen and (max-width: 768px) {
  .clip-1 {
    clip-path: none;
  }
}

.clip-2 {
  clip-path: polygon(0% 0%, 35% 0%, 60% 100%, 0% 100%);
}
</style>
