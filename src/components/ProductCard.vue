<script setup lang="ts">
import { computed, toRefs } from "vue";
import Button from "../components/Button.vue";

type Prop = {
  data: any;
};

const props = defineProps<Prop>();

const { data } = toRefs(props);

const minPrice = computed(() => {
  const types = data.value.types;
  return types.sort((a: any, b: any) => {
    if (a.price < b.price) return -1;
    if (a.price > b.price) return 1;
    return 0;
  })[0].price;
});
</script>

<template>
  <div class="overflow-hidden bg-primary rounded shadow-lg hover:bg-gray-200 hover:shadow-xl">
    <div class>
      <img class="object-contain w-full cursor-pointer aspect-square" :src="data.images[0]?.source_url"
        @click="$router.push('/produk/' + data.slug)" />
    </div>

    <div>
      <h6 class="py-5 text-xl font-bold text-center">{{ data.name }}</h6>
      <div class="px-5 pb-5">
        <div>

          <div>
            <div class="text-xs font-bold text-left">Mulai Dari</div>
            <div class="text-lg font-bold">
              Rp. {{ Intl.NumberFormat("ID-id").format(minPrice) }}
            </div>
          </div>
          <div class="flex justify-center mt-3">
            <Button size="sm" @click="$router.push('/produk/' + data.slug)">Lihat Detail</Button>
          </div>


          <!-- <div class="mt-5">
            <div class="flex items-center gap-2 mt-2 text-xs font-semibold">
              <div>
                <img src="/img/gas-station.png" class="w-6 h-6" />
              </div>
              <div>{{ fuels }}</div>
            </div>

            <div class="flex items-center gap-3 mt-3 text-xs font-semibold">
              <div>
                <img src="/img/manual-transmission.png" class="w-6 h-6" />
              </div>
              <div>
                <p>Transmission</p>
                <p>{{ transmissions }}</p>
              </div>
            </div>
          </div>-->
        </div>
      </div>
    </div>
  </div>
</template>
