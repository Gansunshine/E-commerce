<script lang="ts" setup>
import { useAuthStore } from "~/stores/auth";
const authStore = useAuthStore();
const isAuthenticated = ref();
const router = useRouter();
isAuthenticated.value = useCookie("access_token").value;
const logout = async () => {
  await authStore.logout();
  const accessToken = useCookie("access_token");
  const refreshToken = useCookie("refresh_token");
  accessToken.value = null;
  refreshToken.value = null;
  setTimeout(() => {
    isAuthenticated.value = useCookie("access_token").value;
  }, 100);
  router.push({
    path: "/",
  });
};
</script>

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
            <NuxtLink v-if="!isAuthenticated" to="/login" class="text-base cursor-pointer bg-blue-600 px-6 py-2 text-white rounded-lg hover:bg-blue-600/80">Login</NuxtLink>
            <div v-else class="text-base cursor-pointer bg-red-600 px-6 py-2 text-white rounded-lg hover:bg-red-600/80" @click="logout">Logout</div>
          </nav>
        </div>
      </div>
    </header>
</template>