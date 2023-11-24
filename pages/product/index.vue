<script lang="ts" setup>
import { useProductsStore } from "~/stores/products";

const productStore = useProductsStore();
const { products } = storeToRefs(productStore);
productStore.getAllProducts();

const selectedCategory = ref("");

</script>

<template>
  <section>
    <div class="container">
      <div class="py-10">
        <div class="mb-6 flex justify-end gap-6">
          <NuxtLink to="/product/create" class="bg-green-500 text-white flex justify-center items-center px-3 rounded-lg">
            Create Products</NuxtLink>
          <NuxtLink to="/category/create"
            class="bg-orange-500 text-white flex justify-center items-center px-3 rounded-lg">Create Category</NuxtLink>
          <Dropdown class="md:mb-0 lg:mb-6" @selected-category="selectedCategory = $event" />
        </div>
        <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-4 lg:grid-cols-4 xl:grid-cols-4 gap-4">
          <template v-for="(product, index) in products" :key="index">
            <CardsCardProduct :product="product" class="w-[calc(100%/4-18px)]" />
          </template>
        </div>
      </div>
    </div>
  </section>
</template>