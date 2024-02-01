<template>
  <AisInstantSearch :search-client="searchClient" index-name="demo_ecommerce">
    <AisRefinementList :attribute="'categories'"> </AisRefinementList>
    <AisInfiniteHits show-previous>
      <template #loadPrevious="{ isFirstPage, refinePrevious }">
        <button :disabled="isFirstPage" @click="refinePrevious">
          Load less
        </button>
      </template>
      <template v-slot="{ items, refineNext, isLastPage }">
        <div class="cont">
          <div v-for="item in items" :key="item.objectID" class="item">
            {{ item.name }}
            <img :src="item.image ?? item.thumbnail_url" />
            {{ item }}
          </div>
        </div>
        <button :disabled="isLastPage" @click="refineNext">Load more</button>
      </template>
    </AisInfiniteHits>
  </AisInstantSearch>
</template>
<script setup lang="ts">
import algoliasearch from "algoliasearch/lite";
import {
  AisInstantSearch,
  AisRefinementList,
  AisInfiniteHits,
  // @ts-ignore
} from "vue-instantsearch/vue3/es/index.js";

const searchClient = ref(
  algoliasearch("B1G2GM9NG0", "aadef574be1f9252bb48d4ea09b5cfe5"),
);
</script>
