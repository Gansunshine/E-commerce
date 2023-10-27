<script lang="ts" setup>
    import type { Products } from '~/types/products';
    const props = defineProps({
    product: {
    type: Object,
    default: {},
    }
    });
    const oneProduct = ref(props.product);
    const addCart = () => {
    oneProduct.value.isCart = !oneProduct.value.isCart
    let localStorageData = localStorage.getItem("products");
    let productOfCart: Products[] = [];
    if (localStorageData) {
    productOfCart = JSON.parse(localStorageData);
    }
    if (oneProduct.value.isCart) {
    productOfCart.push(oneProduct.value);
    localStorage.setItem("products", JSON.stringify(productOfCart));
    } else {
    productOfCart = productOfCart.filter((item) => item.id !==
    oneProduct.value.id);
    localStorage.setItem("products", JSON.stringify(productOfCart));
    }
    }
</script>

<template>
    <section class="bg-white shadow-xl rounded-xl overflow-hidden">
        <div :class="`w-full h-[200px] p-5 bg-gray-300`">
            <img :src="oneProduct.image" class="w-full h-full object-contain"/>
        </div>
        <div class="px-5 pb-5 pt-9 relative">
            
            <NuxtLink :to="`/product/${oneProduct.id}`" ><h3 class="text-lg font-
            bold mb-4 text-limit limit-2">{{ oneProduct.name }}</h3></NuxtLink>
            
            <div class="flex justify-between items-center">
            <span class="text-sm font-normal">{{ oneProduct.category }}</span>
            <span class="text-sm font-normal">${{ oneProduct.price }}</span>
            </div>
            <div :class="`cursor-pointer absolute -top-5 right-7 w-[50px] h-[50px]
${oneProduct.isCart ? 'bg-blue-600 text-white' : 'bg-white'} shadow-xl

rounded-full flex justify-center items-center hover:bg-blue-600 hover:text-
white transition duration-300`" @click="addCart">

<i class="ri-shopping-cart-2-line"></i>
</div>
        </div>
    </section>
</template>