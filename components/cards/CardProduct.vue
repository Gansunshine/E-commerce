<script lang="ts" setup>
const props = defineProps({
    product: {
        type: Object,
        default: {},
    }
});
const { baseStorageUrl } = useAppConfig();
</script>

<template>
    <section class="bg-white shadow-xl rounded-xl overflow-hidden w-[250px]">
        <div class="relative h-[200px] overflow-hidden">
            <img :src="baseStorageUrl + props.product.image"
                class="w-full h-full object-cover transform scale-105 hover:scale-110 transition-transform" />
        </div>
        <div class="px-5 pb-5 pt-9">
            <NuxtLink :to="`/product/${props.product.id}`">
                <h3 class="text-lg font-bold mb-4 text-limit limit-2 hover:underline">{{ props.product.name }}</h3>
            </NuxtLink>
            <div class="flex justify-between items-center">
                <span class="text-sm font-normal">{{ props.product.category }}</span>
                <span class="text-sm font-normal">${{ props.product.price }}</span>
            </div>
            <div
                :class="`cursor-pointer mt-2 w-[50px] h-[50px] ${props.product.isCart ? 'bg-blue-600 text-white' : 'bg-white'} shadow-xl rounded-full flex justify-center items-center hover:bg-blue-600 hover:text-white transition duration-300`">
                <i class="ri-shopping-cart-2-line"></i>
            </div>
        </div>
    </section>
</template>
  