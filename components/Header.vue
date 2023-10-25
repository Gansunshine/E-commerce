<template>
    <header class="w-full bg-blue-500 py-4 bg-gray-900" >
      <div class="container mx-auto">
        <div class="flex justify-between items-center">
          <div>
            <NuxtLink to="/" class="text-3xl font-extrabold text-white">SMK Coding</NuxtLink>
          </div>
          <nav class="flex items-center gap-10">
            <NuxtLink to="/" class="text-xl text-white hover:text-blue-300">Home</NuxtLink>
            <NuxtLink to="/product" class="text-xl text-white hover:text-blue-300">Products</NuxtLink>
            <NuxtLink to="/cart" class="text-xl text-white hover:text-blue-300">Cart</NuxtLink>
          </nav>
        </div>
      </div>
    </header>
  </template>
  