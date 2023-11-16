<script setup>
import { defineAsyncComponent } from "vue";

const AsyncStickerResearch = defineAsyncComponent(() =>
    import('./AsyncStickerResearch.vue')
);

</script>

<template>
  <div class="flex flex-col justify-center items-center mt-36">
    <h1 class="text-3xl font-bold mb-4">Das große Disney-100 Sticker-Sammeln der 4BI</h1>

    <Suspense>
      <template #default>
        <AsyncStickerResearch />
      </template>
      <template #fallback>
        <p class="text-xl font-medium">Loading...</p>
      </template>
    </Suspense>

    <div class="fixed bottom-0 mb-10">
      <button class="bg-green-600 text-white font-bold py-2 px-4 rounded mr-10"><a href="https://htl3r-my.sharepoint.com/:x:/g/personal/0212_htl_rennweg_at/EdPVnY_LQFxPqIQR447hCMABuMT-_lISGcTAzzenfwQh3Q?e=cey22i" target="_blank">Fehlende als Excel</a></button>
      <button class="bg-green-600 text-white font-bold py-2 px-4 rounded"><a href="https://htl3r-my.sharepoint.com/:x:/g/personal/0212_htl_rennweg_at/ETuNs2z6NPpNo0i1rVKVx-gBaxKez5BN7RbwuM3xmbOQ3g?e=3vrEEI" target="_blank">Doppelte als Excel</a></button>
    </div>
  </div>
</template>

<style scoped>


</style>
