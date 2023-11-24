<script lang="ts" setup>
import { useCategoryStore } from '~/stores/category';
const categoryStore = useCategoryStore();
const { categories } = storeToRefs(categoryStore);
const isSuccess = ref(false);
const message = ref ("");
const form = ref({
  name: "",
});
const isShowAlert = ref(false);
const createCategory = async () => {
  const newCategoryData = {
    name: form.value.name,
    // Add other properties if needed
  };

  try {
    await categoryStore.createCategory(newCategoryData);

    if (categoryStore.status) {
      isSuccess.value = true;
      message.value = "Category created successfully";
      isShowAlert.value = true;
      form.value.name = "";

      setTimeout(() => {
        isShowAlert.value = false;
      }, 3000);
    } else {
      isSuccess.value = false;
      message.value = "Create Category Failed !!!";
      isShowAlert.value = true;
    }
  } catch (error) {
    isSuccess.value = false;
    isShowAlert.value = true;
  }
};
</script>
<template>
  <section class="flex justify-center py-10">
    <div class="w-[500px]">
      <h1 class="text-2xl mb-7 font-medium">Create Category</h1>
      <div v-if="isShowAlert" class="p-4 mb-4 text-sm rounded-lg ${isSuccess ? 'bg-green-100 text-green-800' : 'text-red-800 bg-red-100'}" role="alert">
        {{ message }}
      </div>
      <form @submit.prevent="createCategory">
        <div class="mb-6">
          <label
            for="name"
            class="block mb-2 text-sm font-medium text-gray- 900"
            >Name</label
          >

          <input
            type="text"
            id="name"
            v-model="form.name"
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
            placeholder="Masukan Nama Category"
            required="true"
          />
        </div>
        <button
          type="submit"
          class="text-white bg-primary hover:bg-primary/80 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center">
          Submit
        </button>
      </form>
    </div>
  </section>
</template>